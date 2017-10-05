---
title: "Exploration et modélisation avancées de données avec Spark | Microsoft Docs"
description: "Utilisez HDInsight Spark pour effectuer l’exploration des données et former des modèles de régression et de classification binaire à l’aide de la validation croisée et de l’optimisation hyperparamétrique."
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
ms.openlocfilehash: e6bf6bd3c905f077841ef166540337a251b91ad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="1406d-103">Modélisation et exploration avancées des données avec Spark</span><span class="sxs-lookup"><span data-stu-id="1406d-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="1406d-104">Cette procédure utilise HDInsight Spark pour effectuer l’exploration des données et former des modèles de régression et de classification binaire à l’aide de la validation croisée et de l’optimisation hyperparamétrique sur un échantillon du jeu de données NYC Taxi Trip and Fare 2013.</span><span class="sxs-lookup"><span data-stu-id="1406d-104">This walkthrough uses HDInsight Spark to do data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of the NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="1406d-105">Elle vous guide tout au long des étapes du [processus de science des données](http://aka.ms/datascienceprocess), à l’aide d’un cluster HDInsight Spark pour le traitement et d’objets blob Azure pour stocker les données et les modèles.</span><span class="sxs-lookup"><span data-stu-id="1406d-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span></span> <span data-ttu-id="1406d-106">Le processus explore et visualise les données importées à partir d’un objet blob Azure Storage, puis prépare les données pour créer des modèles prédictifs.</span><span class="sxs-lookup"><span data-stu-id="1406d-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span></span> <span data-ttu-id="1406d-107">Python a été utilisé pour coder la solution et montrer les tracés correspondants.</span><span class="sxs-lookup"><span data-stu-id="1406d-107">Python has been used to code the solution and to show the relevant plots.</span></span> <span data-ttu-id="1406d-108">Ces modèles sont créés à l’aide de la boîte à outils Spark MLlib pour effectuer des tâches de classification binaire et de modélisation de régression.</span><span class="sxs-lookup"><span data-stu-id="1406d-108">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="1406d-109">La **classification binaire** consiste à prédire si le trajet va faire l’objet d’un pourboire.</span><span class="sxs-lookup"><span data-stu-id="1406d-109">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span></span> 
* <span data-ttu-id="1406d-110">La tâche de **régression** consiste à prédire le montant du pourboire en fonction d’autres critères.</span><span class="sxs-lookup"><span data-stu-id="1406d-110">The **regression** task is to predict the amount of the tip based on other tip features.</span></span> 

<span data-ttu-id="1406d-111">Les étapes de modélisation contiennent également du code montrant comment former, évaluer et enregistrer chaque type de modèle.</span><span class="sxs-lookup"><span data-stu-id="1406d-111">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span></span> <span data-ttu-id="1406d-112">La rubrique traite de certains des thèmes également abordés dans la rubrique [Exploration et modélisation des données avec Spark](machine-learning-data-science-spark-data-exploration-modeling.md).</span><span class="sxs-lookup"><span data-stu-id="1406d-112">The topic covers some of the same ground as the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="1406d-113">Elle est toutefois plus « avancée », dans la mesure où elle utilise également une validation croisée avec un balayage hyperparamétrique pour former des modèles de classification et de régression d’une précision optimale.</span><span class="sxs-lookup"><span data-stu-id="1406d-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping to train optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="1406d-114">La **validation croisée** est une technique qui évalue la manière dont un modèle formé sur un jeu connu de données généralise pour prédire les caractéristiques d’un jeu de données sur lequel il n’a pas été formé.</span><span class="sxs-lookup"><span data-stu-id="1406d-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes to predicting the features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="1406d-115">Une implémentation commune utilisée ici consiste à diviser un jeu de données en plis « K », puis de former le modèle par la méthode tourniquet (round robin) sur tous les plis sauf un.</span><span class="sxs-lookup"><span data-stu-id="1406d-115">A common implementation used here is to divide a dataset into K folds and then train the model in a round-robin fashion on all but one of the folds.</span></span> <span data-ttu-id="1406d-116">La capacité du modèle à offrir des prédictions précises est évaluée lorsqu’il est testé par rapport au jeu de données indépendant de ce pli.</span><span class="sxs-lookup"><span data-stu-id="1406d-116">The ability of the model to prediction accurately when tested against the independent dataset in this fold not used to train the model is assessed.</span></span>

<span data-ttu-id="1406d-117">**optimisation hyperparamétrique** consiste à choisir un jeu d’hyperparamètres pour un algorithme d’apprentissage, généralement dans le but d’optimiser la mesure des performances de l’algorithme sur un jeu de données indépendant.</span><span class="sxs-lookup"><span data-stu-id="1406d-117">**Hyperparameter optimization** is the problem of choosing a set of hyperparameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span></span> <span data-ttu-id="1406d-118">**hyperparamètres** sont des valeurs qui doivent être spécifiées en dehors de la procédure de formation de modèle.</span><span class="sxs-lookup"><span data-stu-id="1406d-118">**Hyperparameters** are values that must be specified outside of the model training procedure.</span></span> <span data-ttu-id="1406d-119">Les hypothèses concernant ces valeurs peuvent avoir un impact sur la flexibilité et la précision des modèles.</span><span class="sxs-lookup"><span data-stu-id="1406d-119">Assumptions about these values can impact the flexibility and accuracy of the models.</span></span> <span data-ttu-id="1406d-120">Les arbres de décision ont des hyperparamètres, tels que la profondeur voulue et le nombre de feuilles de l’arbre.</span><span class="sxs-lookup"><span data-stu-id="1406d-120">Decision trees have hyperparameters, for example, such as the desired depth and number of leaves in the tree.</span></span> <span data-ttu-id="1406d-121">Les machines à vecteurs de support nécessitent la configuration d’un terme de pénalité en cas d’erreur de classification.</span><span class="sxs-lookup"><span data-stu-id="1406d-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="1406d-122">Une façon courante d’effectuer l’optimisation hyperparamétrique, utilisée ici, est la recherche par grille, ou **un balayage paramétrique**.</span><span class="sxs-lookup"><span data-stu-id="1406d-122">A common way to perform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="1406d-123">Elle consiste à effectuer une recherche exhaustive d’un algorithme d’apprentissage sur les valeurs d’un sous-ensemble spécifié de l’espace hyperparamétrique.</span><span class="sxs-lookup"><span data-stu-id="1406d-123">This consists of performing an exhaustive search through the values a specified subset of the hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="1406d-124">La validation croisée peut fournir une mesure de performance permettant de trier les résultats optimaux produits par l’algorithme de recherche par grille.</span><span class="sxs-lookup"><span data-stu-id="1406d-124">Cross validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span></span> <span data-ttu-id="1406d-125">La validation croisée, utilisée avec le balayage hyperparamétrique, limite les problèmes tels que le surajustement d’un modèle aux données de formation ; le modèle peut ainsi être appliqué au jeu de données général à partir duquel les données de formation ont été extraites.</span><span class="sxs-lookup"><span data-stu-id="1406d-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model to training data so that the model retains the capacity to apply to the general set of data from which the training data was extracted.</span></span>

<span data-ttu-id="1406d-126">Les modèles que nous utilisons incluent une régression logistique, une régression linéaire, des forêts aléatoires et des arbres GBT (Gradient Boosted Tree) :</span><span class="sxs-lookup"><span data-stu-id="1406d-126">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="1406d-127">[régression linéaire avec SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) est un modèle de régression linéaire qui utilise la méthode SGD (Stochastic Gradient Descent), l’optimisation et la mise à l’échelle des caractéristiques pour prédire le montant des pourboires payés.</span><span class="sxs-lookup"><span data-stu-id="1406d-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span></span> 
* <span data-ttu-id="1406d-128">[régression logistique avec LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) , ou régression « logit », est un modèle de régression qui s’utilise quand la variable dépendante est catégorielle, pour la classification des données.</span><span class="sxs-lookup"><span data-stu-id="1406d-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span></span> <span data-ttu-id="1406d-129">LBFGS est un algorithme d’optimisation de Quasi-Newton qui correspond approximativement à l’algorithme BFGS (Broyden–Fletcher–Goldfarb–Shanno) avec une quantité limitée de mémoire informatique et qui est largement utilisé dans l’apprentissage automatique (Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="1406d-129">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="1406d-130">[forêts aléatoires](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sont des ensembles d’arbres de décision.</span><span class="sxs-lookup"><span data-stu-id="1406d-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="1406d-131">Elles combinent de nombreux arbres de décision pour réduire le risque de surajustement.</span><span class="sxs-lookup"><span data-stu-id="1406d-131">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="1406d-132">Les forêts aléatoires sont utilisées pour la régression et la classification, peuvent gérer des caractéristiques catégorielles, et peuvent être étendues au paramètre de classification multiclasse.</span><span class="sxs-lookup"><span data-stu-id="1406d-132">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span></span> <span data-ttu-id="1406d-133">Elles ne requièrent aucune mise à l’échelle des caractéristiques, et peuvent capturer des non-linéarités ainsi que des interactions entre caractéristiques.</span><span class="sxs-lookup"><span data-stu-id="1406d-133">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="1406d-134">Les forêts aléatoires constituent l’un des modèles Machine Learning les plus performants pour la classification et la régression.</span><span class="sxs-lookup"><span data-stu-id="1406d-134">Random forests are one of the most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="1406d-135">[Gradient Boosting Tree](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) ) sont des ensembles d’arbres de décision.</span><span class="sxs-lookup"><span data-stu-id="1406d-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="1406d-136">Ils aident les arbres de décision à minimiser itérativement une fonction de perte.</span><span class="sxs-lookup"><span data-stu-id="1406d-136">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="1406d-137">Utilisés pour la régression et la classification, les arbres GBT gèrent les caractéristiques catégorielles, ne requièrent aucune mise à l’échelle des caractéristiques et peuvent capturer les non-linéarités ainsi que les interactions entre les caractéristiques.</span><span class="sxs-lookup"><span data-stu-id="1406d-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="1406d-138">Ils s’utilisent également dans le paramétrage de classification multiclasse.</span><span class="sxs-lookup"><span data-stu-id="1406d-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="1406d-139">Le problème de classification binaire comporte des exemples de modélisation à l’aide de la validation croisée et du balayage hyperparamétrique.</span><span class="sxs-lookup"><span data-stu-id="1406d-139">Modeling examples using CV and Hyperparameter sweep are shown for the binary classification problem.</span></span> <span data-ttu-id="1406d-140">Des exemples plus simples (sans le balayage paramétrique) sont présentés dans la rubrique principale pour les tâches de régression.</span><span class="sxs-lookup"><span data-stu-id="1406d-140">Simpler examples (without parameter sweeps) are presented in the main topic for regression tasks.</span></span> <span data-ttu-id="1406d-141">L’annexe présente également des exemples de validation utilisant un filet élastique pour la régression linéaire, ainsi que de validation croisée utilisant le balayage paramétrique pour la régression par forêts aléatoires.</span><span class="sxs-lookup"><span data-stu-id="1406d-141">But in the appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="1406d-142">Le **filet élastique** est une méthode de régression régularisée pour l’ajustement des modèles de régression linéaire, combinant de manière linéaire les métriques L1 et L2 en tant que pénalités des méthodes [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) et [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization).</span><span class="sxs-lookup"><span data-stu-id="1406d-142">The **elastic net** is a regularized regression method for fitting linear regression models that linearly combines the L1 and L2 metrics as penalties of the [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="1406d-143">Bien que la boîte à outils Spark MLlib soit conçue pour des jeux de données volumineux, nous utilisons ici par souci de commodité un échantillon relativement petit (environ 30 Mo sur 170 000 lignes, soit 0,1 % du jeu de données NYC d’origine).</span><span class="sxs-lookup"><span data-stu-id="1406d-143">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="1406d-144">L’exercice présenté ici fonctionne efficacement (en environ 10 minutes) sur un cluster HDInsight à 2 nœuds de travail.</span><span class="sxs-lookup"><span data-stu-id="1406d-144">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="1406d-145">Le même code permet de traiter des jeux de données plus volumineux, avec quelques modifications mineures concernant la mise en cache des données dans la mémoire ou l’adaptation de la taille du cluster.</span><span class="sxs-lookup"><span data-stu-id="1406d-145">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="1406d-146">Configuration : clusters et notebooks Spark</span><span class="sxs-lookup"><span data-stu-id="1406d-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="1406d-147">Les étapes de configuration et le code fournis dans cette procédure pas à pas concernent HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="1406d-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="1406d-148">Mais des notebooks Jupyter sont fournis pour les clusters HDInsight Spark 1.6 et Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="1406d-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="1406d-149">Une description des notebooks et des liens vers ceux-ci sont fournis dans le fichier [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) correspondant au dépôt GitHub qui les contient.</span><span class="sxs-lookup"><span data-stu-id="1406d-149">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="1406d-150">En outre, le code présenté ici et dans les notebooks liés est générique et doit fonctionner sur n’importe quel cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="1406d-150">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="1406d-151">Si vous n’utilisez pas HDInsight Spark, les étapes de configuration et de gestion de cluster peuvent être légèrement différentes de celles indiquées ici.</span><span class="sxs-lookup"><span data-stu-id="1406d-151">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="1406d-152">Pour plus de commodité, voici les liens vers les notebooks Jupyter pour Spark 1.6 et 2.0 à exécuter dans le noyau pyspark du serveur du notebook Jupyter :</span><span class="sxs-lookup"><span data-stu-id="1406d-152">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 and 2.0 to be run in the pyspark kernel of the Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="1406d-153">Notebooks Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="1406d-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="1406d-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) : inclut les thèmes du notebook 1 et traite également du développement de modèles à l’aide de l’ajustement des hyperparamètres et de la validation croisée.</span><span class="sxs-lookup"><span data-stu-id="1406d-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="1406d-155">Notebooks Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="1406d-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="1406d-156">[Spark2.0-pySpark3-machine-Learning-Data-science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) : ce fichier fournit des informations sur l’exploration des données, la modélisation et la notation dans les clusters Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="1406d-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="1406d-157">Configuration : emplacements de stockage, bibliothèques et contexte Spark prédéfini</span><span class="sxs-lookup"><span data-stu-id="1406d-157">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="1406d-158">Spark peut lire et écrire dans Azure Blob Storage (également appelé WASB).</span><span class="sxs-lookup"><span data-stu-id="1406d-158">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="1406d-159">Donc, vos données stockées dedans sont exploitables par Spark et les résultats peuvent être stockés à nouveau dans WASB.</span><span class="sxs-lookup"><span data-stu-id="1406d-159">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="1406d-160">Pour enregistrer les modèles ou les fichiers dans WASB, le chemin d’accès doit être correctement spécifié.</span><span class="sxs-lookup"><span data-stu-id="1406d-160">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="1406d-161">Le conteneur par défaut associé au cluster Spark peut être référencé à l’aide d’un chemin commençant par wasb///.</span><span class="sxs-lookup"><span data-stu-id="1406d-161">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="1406d-162">Les autres emplacements sont référencés par wasb://.</span><span class="sxs-lookup"><span data-stu-id="1406d-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="1406d-163">Définir les chemins d’accès aux emplacements de stockage dans WASB</span><span class="sxs-lookup"><span data-stu-id="1406d-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="1406d-164">L’exemple de code suivant spécifie l’emplacement des données à lire et le chemin d’accès au répertoire de stockage dans lequel la sortie du modèle est enregistrée :</span><span class="sxs-lookup"><span data-stu-id="1406d-164">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span></span>

    # SET PATHS TO FILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="1406d-165">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-165">**OUTPUT**</span></span>

<span data-ttu-id="1406d-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="1406d-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="1406d-167">Importer les bibliothèques</span><span class="sxs-lookup"><span data-stu-id="1406d-167">Import libraries</span></span>
<span data-ttu-id="1406d-168">Importez les bibliothèques nécessaires avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="1406d-168">Import necessary libraries with the following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="1406d-169">Contexte Spark prédéfini et commandes magiques PySpark</span><span class="sxs-lookup"><span data-stu-id="1406d-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="1406d-170">Les noyaux PySpark fournis avec les blocs-notes Jupyter comprennent un contexte prédéfini.</span><span class="sxs-lookup"><span data-stu-id="1406d-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="1406d-171">Vous n’avez donc pas besoin de définir explicitement les contextes Spark ou Hive avant de commencer à utiliser l’application que vous développez.</span><span class="sxs-lookup"><span data-stu-id="1406d-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="1406d-172">Ces contextes sont disponibles pour vous par défaut.</span><span class="sxs-lookup"><span data-stu-id="1406d-172">These contexts are available for you by default.</span></span> <span data-ttu-id="1406d-173">Ces contextes sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="1406d-173">These contexts are:</span></span>

* <span data-ttu-id="1406d-174">sc : pour Spark</span><span class="sxs-lookup"><span data-stu-id="1406d-174">sc - for Spark</span></span> 
* <span data-ttu-id="1406d-175">sqlContext : pour Hive</span><span class="sxs-lookup"><span data-stu-id="1406d-175">sqlContext - for Hive</span></span>

<span data-ttu-id="1406d-176">Le noyau PySpark fournit certaines « commandes magiques » prédéfinies, qui sont des commandes spéciales que vous pouvez appeler avec %%.</span><span class="sxs-lookup"><span data-stu-id="1406d-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="1406d-177">Deux de ces commandes sont utilisées dans ces exemples de code.</span><span class="sxs-lookup"><span data-stu-id="1406d-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="1406d-178">**%%local** Indique que le code des lignes suivantes doit être exécuté localement.</span><span class="sxs-lookup"><span data-stu-id="1406d-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span></span> <span data-ttu-id="1406d-179">Le code doit être du code Python valide.</span><span class="sxs-lookup"><span data-stu-id="1406d-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="1406d-180">**%%sql -o <variable name>** Exécute une requête Hive sur sqlContext.</span><span class="sxs-lookup"><span data-stu-id="1406d-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="1406d-181">Si le paramètre -o est transmis, le résultat de la requête est conservé dans le contexte Python %%local en tant que tableau de données Pandas.</span><span class="sxs-lookup"><span data-stu-id="1406d-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="1406d-182">Pour plus d’informations sur les noyaux pour blocs-notes Jupyter et sur les « commandes magiques » qu’ils fournissent, voir [Noyaux disponibles pour les blocs-notes Jupyter avec les clusters HDInsight Spark Linux sur HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="1406d-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="1406d-183">Ingestion de données à partir d’un objet blob public :</span><span class="sxs-lookup"><span data-stu-id="1406d-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="1406d-184">La première étape du processus de science des données consiste à ingérer les données à analyser à partir des sources où elles résident, dans votre environnement de modélisation et d’exploration de données.</span><span class="sxs-lookup"><span data-stu-id="1406d-184">The first step in the data science process is to ingest the data to be analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="1406d-185">Dans cette procédure, cet environnement est Spark.</span><span class="sxs-lookup"><span data-stu-id="1406d-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="1406d-186">Cette section contient le code permettant d’effectuer une série de tâches :</span><span class="sxs-lookup"><span data-stu-id="1406d-186">This section contains the code to complete a series of tasks:</span></span>

* <span data-ttu-id="1406d-187">recevoir l’échantillon de données à modéliser</span><span class="sxs-lookup"><span data-stu-id="1406d-187">ingest the data sample to be modeled</span></span>
* <span data-ttu-id="1406d-188">lire le jeu de données en entrée (stocké dans un fichier TSV)</span><span class="sxs-lookup"><span data-stu-id="1406d-188">read in the input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="1406d-189">formater et nettoyer les données</span><span class="sxs-lookup"><span data-stu-id="1406d-189">format and clean the data</span></span>
* <span data-ttu-id="1406d-190">créer et mettre en cache des objets (RDD ou trames de données) en mémoire</span><span class="sxs-lookup"><span data-stu-id="1406d-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="1406d-191">enregistrer les données en tant que table temporaire dans le contexte SQL.</span><span class="sxs-lookup"><span data-stu-id="1406d-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="1406d-192">Voici le code pour l’ingestion de données.</span><span class="sxs-lookup"><span data-stu-id="1406d-192">Here is the code for data ingestion.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
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

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES THE DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="1406d-193">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-193">**OUTPUT**</span></span>

<span data-ttu-id="1406d-194">Durée d’exécution de la cellule ci-dessus : 276,62 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-194">Time taken to execute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="1406d-195">Exploration et visualisation de données</span><span class="sxs-lookup"><span data-stu-id="1406d-195">Data exploration & visualization</span></span>
<span data-ttu-id="1406d-196">Une fois les données intégrées dans Spark, l’étape suivante du processus de science des données consiste à mieux comprendre les données par l’exploration et la visualisation.</span><span class="sxs-lookup"><span data-stu-id="1406d-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="1406d-197">Dans cette section, nous examinons les données des taxis à l’aide de requêtes SQL, et traçons les variables cibles et les caractéristiques prospectives à vérifier visuellement.</span><span class="sxs-lookup"><span data-stu-id="1406d-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="1406d-198">Plus précisément, nous traçons la fréquence des nombres de passagers dans les trajets en taxi, la fréquence des montants des pourboires et la variation des pourboires par type et par montant.</span><span class="sxs-lookup"><span data-stu-id="1406d-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-the-sample-of-taxi-trips"></a><span data-ttu-id="1406d-199">Tracer un histogramme des fréquences de nombres de passagers dans l’échantillon des courses de taxi</span><span class="sxs-lookup"><span data-stu-id="1406d-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span></span>
<span data-ttu-id="1406d-200">Ce code et les extraits de code suivants utilisent une commande magique SQL pour interroger l’exemple et une commande magique locale pour tracer les données.</span><span class="sxs-lookup"><span data-stu-id="1406d-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span></span>

* <span data-ttu-id="1406d-201">**Commande magique SQL (`%%sql`)** Le noyau HDInsight PySpark prend en charge les requêtes HiveQL inline faciles exécutées sur sqlContext.</span><span class="sxs-lookup"><span data-stu-id="1406d-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span></span> <span data-ttu-id="1406d-202">L’argument (-o nom_variable) conserve la sortie de la requête SQL en tant que tableau de données Pandas sur le serveur Jupyter.</span><span class="sxs-lookup"><span data-stu-id="1406d-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span></span> <span data-ttu-id="1406d-203">Cela signifie qu’elle sera disponible en mode local.</span><span class="sxs-lookup"><span data-stu-id="1406d-203">This means it is available in the local mode.</span></span>
* <span data-ttu-id="1406d-204">La **`%%local`** est utilisée pour exécuter le code localement sur le serveur Jupyter, qui est le nœud principal du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1406d-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span></span> <span data-ttu-id="1406d-205">En général, vous devez utiliser la commande magique `%%local` après la commande magique `%%sql -o` pour exécuter une requête.</span><span class="sxs-lookup"><span data-stu-id="1406d-205">Typically, you use `%%local` magic after the `%%sql -o` magic is used to run a query.</span></span> <span data-ttu-id="1406d-206">Le paramètre -o persiste dans la sortie de la requête SQL en local.</span><span class="sxs-lookup"><span data-stu-id="1406d-206">The -o parameter would persist the output of the SQL query locally.</span></span> <span data-ttu-id="1406d-207">La commande magique `%%local` déclenche l’ensemble suivant d’extraits de code à exécuter en local sur la sortie des requêtes SQL qui a été rendue persistante localement.</span><span class="sxs-lookup"><span data-stu-id="1406d-207">Then the `%%local` magic triggers the next set of code snippets to run locally against the output of the SQL queries that has been persisted locally.</span></span> <span data-ttu-id="1406d-208">La sortie est affichée automatiquement après l’exécution du code.</span><span class="sxs-lookup"><span data-stu-id="1406d-208">The output is automatically visualized after you run the code.</span></span>

<span data-ttu-id="1406d-209">Cette requête récupère le nombre de trajets par passager.</span><span class="sxs-lookup"><span data-stu-id="1406d-209">This query retrieves the trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="1406d-210">Ce code crée un tableau de données local à partir de la sortie de la requête et il trace les données.</span><span class="sxs-lookup"><span data-stu-id="1406d-210">This code creates a local data-frame from the query output and plots the data.</span></span> <span data-ttu-id="1406d-211">La commande magique `%%local` crée un tableau de données local, `sqlResults`, qui peut être utilisé pour le tracé avec matplotlib.</span><span class="sxs-lookup"><span data-stu-id="1406d-211">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="1406d-212">Cette commande magique PySpark est utilisée plusieurs fois lors de cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="1406d-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="1406d-213">Si la quantité de données est élevée, vous devez échantillonner pour créer un tableau de données adapté à la mémoire locale.</span><span class="sxs-lookup"><span data-stu-id="1406d-213">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES. 
    # CLICK ON THE TYPE OF PLOT TO BE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="1406d-214">Voici le code qui permet de tracer les nombres de trajets par passager.</span><span class="sxs-lookup"><span data-stu-id="1406d-214">Here is the code to plot the trips by passenger counts</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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

<span data-ttu-id="1406d-215">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-215">**OUTPUT**</span></span>

![Fréquence des voyages par nombre de passagers](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="1406d-217">Vous pouvez sélectionner différents types de visualisations (tables, secteurs, lignes, zones ou barres) à l’aide des boutons de menu **Type** dans le notebook.</span><span class="sxs-lookup"><span data-stu-id="1406d-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span></span> <span data-ttu-id="1406d-218">Le graphique à barres est illustré ici.</span><span class="sxs-lookup"><span data-stu-id="1406d-218">The Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="1406d-219">Tracez un histogramme du montant des pourboires et montrez comment le montant du pourboire varie selon le nombre de passagers et le montant des trajets.</span><span class="sxs-lookup"><span data-stu-id="1406d-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="1406d-220">Utilisez une requête SQL pour échantillonner les données.</span><span class="sxs-lookup"><span data-stu-id="1406d-220">Use a SQL query to sample data..</span></span>

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


<span data-ttu-id="1406d-221">Cette cellule de code utilise la requête SQL pour créer trois graphiques de données.</span><span class="sxs-lookup"><span data-stu-id="1406d-221">This code cell uses the SQL query to create three plots the data.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="1406d-222">**SORTIE :**</span><span class="sxs-lookup"><span data-stu-id="1406d-222">**OUTPUT:**</span></span> 

![Distribution des montants de pourboire](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Montant de pourboire par nombre de passagers](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Montant du pourboire par montant de la course](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="1406d-226">Conception des caractéristiques, transformation et préparation des données à modéliser</span><span class="sxs-lookup"><span data-stu-id="1406d-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="1406d-227">Cette section décrit et fournit le code des procédures servant à préparer les données à utiliser dans la modélisation ML.</span><span class="sxs-lookup"><span data-stu-id="1406d-227">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span></span> <span data-ttu-id="1406d-228">Elle montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1406d-228">It shows how to do the following tasks:</span></span>

* <span data-ttu-id="1406d-229">Créer une caractéristique en partitionnant les heures dans des périodes de trafic</span><span class="sxs-lookup"><span data-stu-id="1406d-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="1406d-230">Indexer et encoder des fonctionnalités catégorielles</span><span class="sxs-lookup"><span data-stu-id="1406d-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="1406d-231">Créer des objets point étiquetés à intégrer dans les fonctions ML</span><span class="sxs-lookup"><span data-stu-id="1406d-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="1406d-232">Créer un sous-échantillonnage aléatoire des données et le diviser en un jeu de formation et un jeu de test</span><span class="sxs-lookup"><span data-stu-id="1406d-232">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
* <span data-ttu-id="1406d-233">Mise à l’échelle des caractéristiques</span><span class="sxs-lookup"><span data-stu-id="1406d-233">Feature scaling</span></span>
* <span data-ttu-id="1406d-234">Mettre en cache des objets en mémoire</span><span class="sxs-lookup"><span data-stu-id="1406d-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="1406d-235">Créer une caractéristique en partitionnant les périodes de trafic dans les emplacements</span><span class="sxs-lookup"><span data-stu-id="1406d-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="1406d-236">Ce code montre comment créer une nouvelle caractéristique en partitionnant les périodes de trafic et comment mettre en cache la trame de données obtenue en mémoire.</span><span class="sxs-lookup"><span data-stu-id="1406d-236">This code shows how to create a new feature by partitioning traffic times into bins and then how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="1406d-237">La mise en cache réduit les temps d’exécution, là où les jeux de données distribués résilients (RDD) et les trames de données sont utilisés de manière répétitive.</span><span class="sxs-lookup"><span data-stu-id="1406d-237">Caching leads to improved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="1406d-238">Par conséquent, nous mettons en cache les RDD et les trames de données à plusieurs stades de la procédure.</span><span class="sxs-lookup"><span data-stu-id="1406d-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

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
    # THE .COUNT() GOES THROUGH THE ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES THE COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="1406d-239">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-239">**OUTPUT**</span></span>

<span data-ttu-id="1406d-240">126050</span><span class="sxs-lookup"><span data-stu-id="1406d-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="1406d-241">Indexer et encoder « à chaud » des fonctionnalités catégorielles</span><span class="sxs-lookup"><span data-stu-id="1406d-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="1406d-242">Cette section montre comment indexer ou encoder les caractéristiques catégorielles à intégrer dans les fonctions de modélisation.</span><span class="sxs-lookup"><span data-stu-id="1406d-242">This section shows how to index or encode categorical features for input into the modeling functions.</span></span> <span data-ttu-id="1406d-243">Les fonctions de modélisation et de prédiction de MLlib requièrent des caractéristiques avec des données d’entrée catégorielles à indexer ou à encoder avant leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="1406d-243">The modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior to use.</span></span> 

<span data-ttu-id="1406d-244">Selon le modèle, vous devez les indexer ou les encoder différemment :</span><span class="sxs-lookup"><span data-stu-id="1406d-244">Depending on the model, you need to index or encode them in different ways.</span></span> <span data-ttu-id="1406d-245">Les modèles de régression logistique et linéaire requièrent un encodage linéaire où, par exemple, une fonction avec trois catégories peut être développée en trois colonnes de caractéristiques, chacune contenant 0 ou 1, selon la catégorie d’une observation.</span><span class="sxs-lookup"><span data-stu-id="1406d-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="1406d-246">MLlib fournit la fonction [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) permettant d’effectuer un encodage linéaire.</span><span class="sxs-lookup"><span data-stu-id="1406d-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span></span> <span data-ttu-id="1406d-247">Cet encodeur mappe une colonne d’index de libellé à une colonne de vecteurs binaires, contenant au plus une seule une valeur.</span><span class="sxs-lookup"><span data-stu-id="1406d-247">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="1406d-248">Cet encodage autorise les algorithmes qui attentent des caractéristiques numériques, comme une régression logistique, à appliquer à des caractéristiques catégorielles.</span><span class="sxs-lookup"><span data-stu-id="1406d-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span></span>

<span data-ttu-id="1406d-249">Voici le code permettant d’indexer et d’encoder des caractéristiques catégorielles :</span><span class="sxs-lookup"><span data-stu-id="1406d-249">Here is the code to index and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is the cleaned one from above
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="1406d-250">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-250">**OUTPUT**</span></span>

<span data-ttu-id="1406d-251">Durée d’exécution de la cellule ci-dessus : 3,14 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-251">Time taken to execute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="1406d-252">Créer des objets point étiquetés à intégrer dans les fonctions ML</span><span class="sxs-lookup"><span data-stu-id="1406d-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="1406d-253">Cette section contient le code qui montre comment indexer les données catégoriques de texte comme type de données de point étiquetées et comment les encoder.</span><span class="sxs-lookup"><span data-stu-id="1406d-253">This section contains code that shows how to index categorical text data as a labeled point data type and how to encode it.</span></span> <span data-ttu-id="1406d-254">Elles sont ainsi préparer pour l’apprentissage et le test de la régression logistique MLlib et d’autres modèles de classification.</span><span class="sxs-lookup"><span data-stu-id="1406d-254">This prepares it to be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="1406d-255">Les objets point étiquetés sont des jeux de données distribués résilients (RDD) mis en forme en tant que données d’entrée utilisables par la plupart des algorithmes ML dans MLlib.</span><span class="sxs-lookup"><span data-stu-id="1406d-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="1406d-256">Un [point étiqueté](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) est un vecteur local, dense ou fragmenté, associé à un libellé/une réponse.</span><span class="sxs-lookup"><span data-stu-id="1406d-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="1406d-257">Voici le code qui permet d’indexer et d’encoder des caractéristiques textuelles pour la classification binaire.</span><span class="sxs-lookup"><span data-stu-id="1406d-257">Here is the code to index and encode text features for binary classification.</span></span>

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


<span data-ttu-id="1406d-258">Voici le code qui permet d’encoder des caractéristiques textuelles par catégorie d’index pour l’analyse de régression linéaire.</span><span class="sxs-lookup"><span data-stu-id="1406d-258">Here is the code to encode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-the-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="1406d-259">Créer un sous-échantillonnage aléatoire des données et le diviser en un jeu de formation et un jeu de test</span><span class="sxs-lookup"><span data-stu-id="1406d-259">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
<span data-ttu-id="1406d-260">Ce code crée un échantillonnage aléatoire des données (25 % utilisé ici).</span><span class="sxs-lookup"><span data-stu-id="1406d-260">This code creates a random sampling of the data (25% is used here).</span></span> <span data-ttu-id="1406d-261">Bien que ce ne soit pas nécessaire dans cet exemple en raison de la taille du jeu de données, nous vous montrons ici comment créer un échantillon.</span><span class="sxs-lookup"><span data-stu-id="1406d-261">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample the data here.</span></span> <span data-ttu-id="1406d-262">Vous saurez ainsi comment l’utiliser pour votre propre problème si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1406d-262">Then you know how to use it for your own problem if needed.</span></span> <span data-ttu-id="1406d-263">Lorsque les échantillons sont volumineux, cela permet de gagner beaucoup de temps pendant l’apprentissage des modèles.</span><span class="sxs-lookup"><span data-stu-id="1406d-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="1406d-264">Ensuite, nous divisons l’échantillon en une partie d’apprentissage (75 % ici) et une partie de test (25 % ici) à utiliser dans la modélisation de la classification et de la régression.</span><span class="sxs-lookup"><span data-stu-id="1406d-264">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="1406d-265">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-265">**OUTPUT**</span></span>

<span data-ttu-id="1406d-266">Durée d’exécution de la cellule ci-dessus : 0,31 seconde</span><span class="sxs-lookup"><span data-stu-id="1406d-266">Time taken to execute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="1406d-267">Mise à l’échelle des caractéristiques</span><span class="sxs-lookup"><span data-stu-id="1406d-267">Feature scaling</span></span>
<span data-ttu-id="1406d-268">La mise à l’échelle des caractéristiques, également appelée normalisation des données, garantit que les caractéristiques aux valeurs très dispersées sont pondérées dans la fonction cible.</span><span class="sxs-lookup"><span data-stu-id="1406d-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> <span data-ttu-id="1406d-269">Le code de mise à l’échelle des caractéristiques utilise [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) pour mettre à l’échelle les caractéristiques à la variance d’unité.</span><span class="sxs-lookup"><span data-stu-id="1406d-269">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span></span> <span data-ttu-id="1406d-270">MLlib le fournit en vue d’une utilisation dans une régression linéaire avec SGD (Stochastic Gradient Descent).</span><span class="sxs-lookup"><span data-stu-id="1406d-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="1406d-271">SGD est un algorithme populaire permettant de former une large gamme d’autres modèles Machine Learning, tels que les régressions régularisées ou les machines à vecteurs de support (SVM).</span><span class="sxs-lookup"><span data-stu-id="1406d-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="1406d-272">Nous avons découvert que l’algorithme LinearRegressionWithSGD est sensible à la mise à l’échelle des caractéristiques.</span><span class="sxs-lookup"><span data-stu-id="1406d-272">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span></span>   
> 
> 

<span data-ttu-id="1406d-273">Voici le code pour mettre à l’échelle des variables pour l’algorithme pour une utilisation avec l’algorithme SGD linéaire régularisé.</span><span class="sxs-lookup"><span data-stu-id="1406d-273">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="1406d-274">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-274">**OUTPUT**</span></span>

<span data-ttu-id="1406d-275">Durée d’exécution de la cellule ci-dessus : 11,67 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-275">Time taken to execute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="1406d-276">Mettre en cache des objets en mémoire</span><span class="sxs-lookup"><span data-stu-id="1406d-276">Cache objects in memory</span></span>
<span data-ttu-id="1406d-277">La durée d’apprentissage et de test des algorithmes ML peut être réduite par la mise en cache d’objets de trame de données utilisés pour la classification, la régression et les caractéristiques mises à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="1406d-277">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression and, scaled features.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="1406d-278">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-278">**OUTPUT**</span></span> 

<span data-ttu-id="1406d-279">Durée d’exécution de la cellule ci-dessus : 0,13 seconde</span><span class="sxs-lookup"><span data-stu-id="1406d-279">Time taken to execute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="1406d-280">Prédire si un pourboire a été payé avec des modèles de classification binaires</span><span class="sxs-lookup"><span data-stu-id="1406d-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="1406d-281">Cette section montre comment utiliser trois modèles de tâche de classification binaire pour prédire si un pourboire est payé pour une course en taxi.</span><span class="sxs-lookup"><span data-stu-id="1406d-281">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="1406d-282">Les modèles présentés sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="1406d-282">The models presented are:</span></span>

* <span data-ttu-id="1406d-283">Régression logique</span><span class="sxs-lookup"><span data-stu-id="1406d-283">Logistic regression</span></span> 
* <span data-ttu-id="1406d-284">Forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="1406d-284">Random forest</span></span>
* <span data-ttu-id="1406d-285">Arbres GBT (Gradient Boosting Tree)</span><span class="sxs-lookup"><span data-stu-id="1406d-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="1406d-286">Chaque section de code générateur de modèle est divisée en étapes :</span><span class="sxs-lookup"><span data-stu-id="1406d-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="1406d-287">**formation du modèle** avec un jeu de paramètres</span><span class="sxs-lookup"><span data-stu-id="1406d-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="1406d-288">**Évaluation de modèle** sur un jeu de données de test avec mesures</span><span class="sxs-lookup"><span data-stu-id="1406d-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="1406d-289">**Enregistrement du modèle** dans l’objet blob en vue d’une utilisation ultérieure</span><span class="sxs-lookup"><span data-stu-id="1406d-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="1406d-290">Nous présentons la validation croisée avec le balayage paramétrique de deux manières :</span><span class="sxs-lookup"><span data-stu-id="1406d-290">We show how to do cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="1406d-291">À l’aide de code personnalisé **générique** pouvant être appliqué à n’importe quel algorithme de MLlib et à n’importe quel jeu de paramètres dans un algorithme.</span><span class="sxs-lookup"><span data-stu-id="1406d-291">Using **generic** custom code which can be applied to any algorithm in MLlib and to any parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="1406d-292">À l’aide de la **fonction pipeline pySpark CrossValidator**.</span><span class="sxs-lookup"><span data-stu-id="1406d-292">Using the **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="1406d-293">Notez que CrossValidator présente quelques limitations pour Spark 1.5.0 :</span><span class="sxs-lookup"><span data-stu-id="1406d-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="1406d-294">Les modèles de pipeline ne peuvent pas être enregistrés/conservés pour une consommation future.</span><span class="sxs-lookup"><span data-stu-id="1406d-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="1406d-295">Ne peut pas être utilisé pour chaque paramètre dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="1406d-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="1406d-296">Ne peut pas être utilisé pour chaque algorithme MLlib.</span><span class="sxs-lookup"><span data-stu-id="1406d-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-the-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="1406d-297">Validation croisée générique et balayage paramétrique utilisés avec l’algorithme de régression logistique pour la classification binaire</span><span class="sxs-lookup"><span data-stu-id="1406d-297">Generic cross validation and hyperparameter sweeping used with the logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="1406d-298">Le code de cette section montre comment former, évaluer et enregistrer un modèle de régression logistique avec [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , qui prédit si un pourboire est payé pour un trajet dans le jeu de données des courses et tarifs de taxi à New York.</span><span class="sxs-lookup"><span data-stu-id="1406d-298">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="1406d-299">Le modèle est formé à l’aide de la validation croisée et le balayage paramétrique, implémentés avec du code personnalisé pouvant être appliqué à un algorithme d’apprentissage quelconque dans MLlib.</span><span class="sxs-lookup"><span data-stu-id="1406d-299">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied to any of the learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="1406d-300">L’exécution de ce code de validation croisée personnalisé peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="1406d-300">The execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="1406d-301">**Former le modèle de régression logistique à l’aide de la validation croisée et du balayage hyperparamétrique**</span><span class="sxs-lookup"><span data-stu-id="1406d-301">**Train the logistic regression model using CV and hyperparameter sweeping**</span></span>

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

    # SET NUM FOLDS AND NUM PARAMETER SETS TO SWEEP ON
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


    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="1406d-302">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-302">**OUTPUT**</span></span>

<span data-ttu-id="1406d-303">Coefficients : [0,0082065285375, -0,0223675576104, -0,0183812028036, -3.48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]</span><span class="sxs-lookup"><span data-stu-id="1406d-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="1406d-304">Interception : -0,0111216486893</span><span class="sxs-lookup"><span data-stu-id="1406d-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="1406d-305">Durée d’exécution de la cellule ci-dessus : 14,43 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-305">Time taken to execute above cell: 14.43 seconds</span></span>

<span data-ttu-id="1406d-306">**Évaluer le modèle de classification binaire avec des mesures standard**</span><span class="sxs-lookup"><span data-stu-id="1406d-306">**Evaluate the binary classification model with standard metrics**</span></span>

<span data-ttu-id="1406d-307">Le code de cette section montre comment évaluer un modèle de régression logistique par rapport à un jeu de données de test, y compris un tracé de la courbe ROC.</span><span class="sxs-lookup"><span data-stu-id="1406d-307">The code in this section shows how to evaluate a logistic regression model against a test data-set, including a plot of the ROC curve.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="1406d-308">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-308">**OUTPUT**</span></span>

<span data-ttu-id="1406d-309">Zone sous PR = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="1406d-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="1406d-310">Zone sous ROC = 0,983383274312</span><span class="sxs-lookup"><span data-stu-id="1406d-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="1406d-311">Résumé des statistiques</span><span class="sxs-lookup"><span data-stu-id="1406d-311">Summary Stats</span></span>

<span data-ttu-id="1406d-312">Précision = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="1406d-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="1406d-313">Rappel = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="1406d-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="1406d-314">Score F1 = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="1406d-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="1406d-315">Durée d’exécution de la cellule ci-dessus : 2,67 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-315">Time taken to execute above cell: 2.67 seconds</span></span>

<span data-ttu-id="1406d-316">**Tracer la courbe ROC.**</span><span class="sxs-lookup"><span data-stu-id="1406d-316">**Plot the ROC curve.**</span></span>

<span data-ttu-id="1406d-317">*predictionAndLabelsDF* est inscrit en tant que table, *tmp_results*, dans la cellule précédente.</span><span class="sxs-lookup"><span data-stu-id="1406d-317">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="1406d-318">*tmp_results* peut être utilisé pour effectuer des requêtes et envoyer des résultats à la trame de données sqlResults à des fins de traçage.</span><span class="sxs-lookup"><span data-stu-id="1406d-318">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="1406d-319">Voici le code.</span><span class="sxs-lookup"><span data-stu-id="1406d-319">Here is the code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="1406d-320">Voici le code permettant d’effectuer des prédictions et de tracer la courbe ROC.</span><span class="sxs-lookup"><span data-stu-id="1406d-320">Here is the code to make predictions and plot the ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES                              
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


<span data-ttu-id="1406d-321">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-321">**OUTPUT**</span></span>

![Courbe ROC de régression logistique pour une approche générique](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="1406d-323">**Conservation du modèle dans un objet blob en vue d’une consommation ultérieure**</span><span class="sxs-lookup"><span data-stu-id="1406d-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="1406d-324">Le code de cette section montre comment enregistrer le modèle de régression logistique en vue d’une consommation.</span><span class="sxs-lookup"><span data-stu-id="1406d-324">The code in this section shows how to save the logistic regression model for consumption.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="1406d-325">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-325">**OUTPUT**</span></span>

<span data-ttu-id="1406d-326">Durée d’exécution de la cellule ci-dessus : 34,57 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-326">Time taken to execute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="1406d-327">Utiliser la fonction pipeline CrossValidator de MLlib avec le modèle LogisticRegression (régression élastique)</span><span class="sxs-lookup"><span data-stu-id="1406d-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="1406d-328">Le code de cette section montre comment former, évaluer et enregistrer un modèle de régression logistique avec [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , qui prédit si un pourboire est payé pour un trajet dans le jeu de données des courses et tarifs de taxi à New York.</span><span class="sxs-lookup"><span data-stu-id="1406d-328">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="1406d-329">Le modèle est formé à l’aide de la validation croisée et du balayage hyperparamétrique, implémentés par la fonction pipeline MLlib CrossValidator pour la validation croisée avec le balayage paramétrique.</span><span class="sxs-lookup"><span data-stu-id="1406d-329">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with the MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="1406d-330">L’exécution de ce code de validation croisée MLlib peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="1406d-330">The execution of this MLlib CV code can take several minutes.</span></span>
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

    # CONVERT TO DATA-FRAME: THIS DOES NOT RUN ON RDDs
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="1406d-331">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-331">**OUTPUT**</span></span>

<span data-ttu-id="1406d-332">Durée d’exécution de la cellule ci-dessus : 107,98 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-332">Time taken to execute above cell: 107.98 seconds</span></span>

<span data-ttu-id="1406d-333">**Tracer la courbe ROC.**</span><span class="sxs-lookup"><span data-stu-id="1406d-333">**Plot the ROC curve.**</span></span>

<span data-ttu-id="1406d-334">*predictionAndLabelsDF* est inscrit en tant que table, *tmp_results*, dans la cellule précédente.</span><span class="sxs-lookup"><span data-stu-id="1406d-334">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="1406d-335">*tmp_results* peut être utilisé pour effectuer des requêtes et envoyer des résultats à la trame de données sqlResults à des fins de traçage.</span><span class="sxs-lookup"><span data-stu-id="1406d-335">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="1406d-336">Voici le code.</span><span class="sxs-lookup"><span data-stu-id="1406d-336">Here is the code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="1406d-337">Voici le code permettant de tracer la courbe ROC.</span><span class="sxs-lookup"><span data-stu-id="1406d-337">Here is the code to plot the ROC curve.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES 
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


<span data-ttu-id="1406d-338">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-338">**OUTPUT**</span></span>

![Courbe ROC de régression logistique utilisant la fonction CrossValidator de MLlib](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="1406d-340">Classification par forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="1406d-340">Random forest classification</span></span>
<span data-ttu-id="1406d-341">Le code de cette section montre comment former, évaluer et enregistrer une régression de forêts aléatoires qui prédit si un pourboire est payé pour un trajet dans le jeu de données des courses et tarifs de taxi à New York.</span><span class="sxs-lookup"><span data-stu-id="1406d-341">The code in this section shows how to train, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT TO PRING TREES
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="1406d-342">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-342">**OUTPUT**</span></span>

<span data-ttu-id="1406d-343">Zone sous ROC = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="1406d-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="1406d-344">Durée d’exécution de la cellule ci-dessus : 26,72 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-344">Time taken to execute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="1406d-345">Classification par arbres GBT (Gradient Boosting Tree)</span><span class="sxs-lookup"><span data-stu-id="1406d-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="1406d-346">Le code de cette section montre comment former, évaluer et enregistrer un modèle d’arbres GBT qui prédit si un pourboire est payé pour un trajet dans le jeu de données des courses et tarifs de taxi à New York.</span><span class="sxs-lookup"><span data-stu-id="1406d-346">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT TO PRINT TREE DETAILS
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="1406d-347">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-347">**OUTPUT**</span></span>

<span data-ttu-id="1406d-348">Zone sous ROC = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="1406d-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="1406d-349">Durée d’exécution de la cellule ci-dessus : 28,13 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-349">Time taken to execute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="1406d-350">Prédire le montant des pourboires avec les modèles de régression (sans la validation croisée)</span><span class="sxs-lookup"><span data-stu-id="1406d-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="1406d-351">Cette section montre comment utiliser trois modèles pour la tâche de régression qui consiste à prédire le montant du pourboire versé pour une course de taxi en fonction d’autres caractéristiques de pourboire.</span><span class="sxs-lookup"><span data-stu-id="1406d-351">This section shows how use three models for the regression task: predict the tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="1406d-352">Les modèles présentés sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="1406d-352">The models presented are:</span></span>

* <span data-ttu-id="1406d-353">Régression linéaire régularisée</span><span class="sxs-lookup"><span data-stu-id="1406d-353">Regularized linear regression</span></span>
* <span data-ttu-id="1406d-354">Forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="1406d-354">Random forest</span></span>
* <span data-ttu-id="1406d-355">Arbres GBT (Gradient Boosting Tree)</span><span class="sxs-lookup"><span data-stu-id="1406d-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="1406d-356">Ces modèles sont décrits dans l’introduction.</span><span class="sxs-lookup"><span data-stu-id="1406d-356">These models were described in the introduction.</span></span> <span data-ttu-id="1406d-357">Chaque section de code générateur de modèle est divisée en étapes :</span><span class="sxs-lookup"><span data-stu-id="1406d-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="1406d-358">**formation du modèle** avec un jeu de paramètres</span><span class="sxs-lookup"><span data-stu-id="1406d-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="1406d-359">**Évaluation de modèle** sur un jeu de données de test avec mesures</span><span class="sxs-lookup"><span data-stu-id="1406d-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="1406d-360">**Enregistrement du modèle** dans l’objet blob en vue d’une utilisation ultérieure</span><span class="sxs-lookup"><span data-stu-id="1406d-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="1406d-361">REMARQUE AZURE : La validation croisée n’est pas utilisée avec les trois modèles de régression dans cette section, car cela a été décrit en détail pour les modèles de régression logistique.</span><span class="sxs-lookup"><span data-stu-id="1406d-361">AZURE NOTE: Cross-validation is not used with the three regression models in this section, since this was shown in detail for the logistic regression models.</span></span> <span data-ttu-id="1406d-362">L’annexe de cette rubrique présente un exemple d’utilisation de la validation croisée avec un filet élastique pour la régression linéaire.</span><span class="sxs-lookup"><span data-stu-id="1406d-362">An example showing how to use CV with Elastic Net for linear regression is provided in the Appendix of this topic.</span></span>
> 
> <span data-ttu-id="1406d-363">REMARQUE AZURE : Selon notre expérience, il peut y avoir des problèmes avec la convergence des modèles LinearRegressionWithSGD, et les paramètres doivent être modifiés/optimisés avec soin pour obtenir un modèle valide.</span><span class="sxs-lookup"><span data-stu-id="1406d-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="1406d-364">La mise à l’échelle des variables est très utile avec la convergence.</span><span class="sxs-lookup"><span data-stu-id="1406d-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="1406d-365">Vous pouvez aussi utiliser la régression élastique nette, présentée dans l’annexe de cette rubrique, au lieu de LinearRegressionWithSGD.</span><span class="sxs-lookup"><span data-stu-id="1406d-365">Elastic net regression, shown in the Appendix to this topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="1406d-366">régression linéaire avec SGD</span><span class="sxs-lookup"><span data-stu-id="1406d-366">Linear regression with SGD</span></span>
<span data-ttu-id="1406d-367">Le code de cette section montre comment utiliser des caractéristiques mises à l’échelle pour former une régression linéaire utilisant utilise la descente de gradient stochastique (SGD) à des fins d’optimisation et comment noter, évaluer et enregistrer le modèle dans Azure Blob Storage (WASB).</span><span class="sxs-lookup"><span data-stu-id="1406d-367">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="1406d-368">D’après notre expérience, il peut y avoir des problèmes avec la convergence des modèles LinearRegressionWithSGD, et les paramètres doivent être modifiés/optimisés avec soin pour obtenir un modèle valide.</span><span class="sxs-lookup"><span data-stu-id="1406d-368">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="1406d-369">La mise à l’échelle des variables est très utile avec la convergence.</span><span class="sxs-lookup"><span data-stu-id="1406d-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES TO TRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="1406d-370">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-370">**OUTPUT**</span></span>

<span data-ttu-id="1406d-371">Coefficients : [0,0141707753435, -0,0252930927087, -0,0231442517137, 0,247070902996, 0,312544147152, 0,360296120645, 0,0122079566092, -0,00456498588241, -0,0898228505177, 0,0714046248793, 0,102171263868, 0,100022455632, -0,00289545676449, -0,00791124681938, 0,54396316518, -0,536293513569, 0,0119076553369, -0,0173039244582, 0,0119632796147, 0,00146764882502]</span><span class="sxs-lookup"><span data-stu-id="1406d-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="1406d-372">Interception : -0,854507624459</span><span class="sxs-lookup"><span data-stu-id="1406d-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="1406d-373">RMSE = 1,23485131376</span><span class="sxs-lookup"><span data-stu-id="1406d-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="1406d-374">Racine carrée = 0,597963951127</span><span class="sxs-lookup"><span data-stu-id="1406d-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="1406d-375">Durée d’exécution de la cellule ci-dessus : 38,62 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-375">Time taken to execute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="1406d-376">Régression par forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="1406d-376">Random Forest regression</span></span>
<span data-ttu-id="1406d-377">Le code de cette section montre comment former, évaluer et enregistrer un modèle de forêts aléatoires qui prédit le montant d’un pourboire pour les données sur les courses de taxi à New York.</span><span class="sxs-lookup"><span data-stu-id="1406d-377">The code in this section shows how to train, evaluate, and save a random forest model that predicts tip amount for the NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="1406d-378">La validation croisée avec le balayage paramétrique, utilisant un code personnalisé, est présentée dans l’annexe.</span><span class="sxs-lookup"><span data-stu-id="1406d-378">Cross-validation with parameter sweeping using custom code is provided in the appendix.</span></span>
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
    # UN-COMMENT IF YOU WANT TO PRING TREES
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="1406d-379">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-379">**OUTPUT**</span></span>

<span data-ttu-id="1406d-380">RMSE = 0,931981967875</span><span class="sxs-lookup"><span data-stu-id="1406d-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="1406d-381">Racine carrée = 0,733445485802</span><span class="sxs-lookup"><span data-stu-id="1406d-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="1406d-382">Durée d’exécution de la cellule ci-dessus : 25,98 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-382">Time taken to execute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="1406d-383">Régression par arbres GBT (Gradient Boosting Tree)</span><span class="sxs-lookup"><span data-stu-id="1406d-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="1406d-384">Le code de cette section montre comment former, évaluer et enregistrer un modèle d’arbres GBT, qui prédit le montant d’un pourboire pour les données sur les courses de taxi à New York.</span><span class="sxs-lookup"><span data-stu-id="1406d-384">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span></span>

<span data-ttu-id="1406d-385">** L’apprentissage et évaluer **</span><span class="sxs-lookup"><span data-stu-id="1406d-385">**Train and evaluate **</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="1406d-386">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-386">**OUTPUT**</span></span>

<span data-ttu-id="1406d-387">RMSE = 0,928172197114</span><span class="sxs-lookup"><span data-stu-id="1406d-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="1406d-388">Racine carrée = 0,732680354389</span><span class="sxs-lookup"><span data-stu-id="1406d-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="1406d-389">Durée d’exécution de la cellule ci-dessus : 20,9 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-389">Time taken to execute above cell: 20.9 seconds</span></span>

<span data-ttu-id="1406d-390">**Tracer**</span><span class="sxs-lookup"><span data-stu-id="1406d-390">**Plot**</span></span>

<span data-ttu-id="1406d-391">*tmp_results* est inscrit en tant que table Hive dans la cellule précédente.</span><span class="sxs-lookup"><span data-stu-id="1406d-391">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="1406d-392">Les résultats de la table sont envoyés à la trame de données *sqlResults* à des fins de traçage.</span><span class="sxs-lookup"><span data-stu-id="1406d-392">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="1406d-393">Voici le code.</span><span class="sxs-lookup"><span data-stu-id="1406d-393">Here is the code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="1406d-394">Voici le code pour tracer les données à l’aide du serveur Jupyter.</span><span class="sxs-lookup"><span data-stu-id="1406d-394">Here is the code to plot the data using the Jupyter server.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="1406d-396">Annexe : Tâches de régression supplémentaires utilisant la validation croisée avec balayage paramétrique</span><span class="sxs-lookup"><span data-stu-id="1406d-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="1406d-397">Cette annexe contient un code présentant la validation croisée utilisant un filet élastique pour la régression linéaire. Elle montre également comment effectuer une validation croisée avec balayage paramétrique à l’aide d’un code personnalisé pour la régression par forêts aléatoires.</span><span class="sxs-lookup"><span data-stu-id="1406d-397">This appendix contains code showing how to do CV using Elastic net for linear regression and how to do CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="1406d-398">Validation croisée à l’aide d’un filet élastique pour la régression linéaire</span><span class="sxs-lookup"><span data-stu-id="1406d-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="1406d-399">Le code dans cette section montre comment effectuer une validation croisée à l’aide d’un filet élastique pour la régression linéaire, et comment évaluer le modèle par rapport aux données de test.</span><span class="sxs-lookup"><span data-stu-id="1406d-399">The code in this section shows how to do cross validation using Elastic net for linear regression and how to evaluate the model against test data.</span></span>

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
    # SIMPLY THE MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT TO DATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses the best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT TO DF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="1406d-400">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-400">**OUTPUT**</span></span>

<span data-ttu-id="1406d-401">Durée d’exécution de la cellule ci-dessus : 161,21 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-401">Time taken to execute above cell: 161.21  seconds</span></span>

<span data-ttu-id="1406d-402">**Évaluer avec la mesure R-SQR**</span><span class="sxs-lookup"><span data-stu-id="1406d-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="1406d-403">*tmp_results* est inscrit en tant que table Hive dans la cellule précédente.</span><span class="sxs-lookup"><span data-stu-id="1406d-403">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="1406d-404">Les résultats de la table sont envoyés à la trame de données *sqlResults* à des fins de traçage.</span><span class="sxs-lookup"><span data-stu-id="1406d-404">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="1406d-405">Voici le code.</span><span class="sxs-lookup"><span data-stu-id="1406d-405">Here is the code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="1406d-406">Voici le code pour calculer R-sqr.</span><span class="sxs-lookup"><span data-stu-id="1406d-406">Here is the code to calculate R-sqr.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="1406d-407">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-407">**OUTPUT**</span></span>

<span data-ttu-id="1406d-408">Racine carrée = 0,619184907088</span><span class="sxs-lookup"><span data-stu-id="1406d-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="1406d-409">Validation croisée avec balayage paramétrique à l’aide de code personnalisé pour la régression par forêts aléatoires</span><span class="sxs-lookup"><span data-stu-id="1406d-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="1406d-410">Le code dans cette section montre comment effectuer une validation croisée avec balayage paramétrique à l’aide d’un code personnalisé pour la régression par forêts aléatoires, et comment évaluer le modèle par rapport aux données de test.</span><span class="sxs-lookup"><span data-stu-id="1406d-410">The code in this section shows how to do cross validation with parameter sweep using custom code for random forest regression and how to evaluate the model against test data.</span></span>

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

    # SPECIFY NUMFOLDS AND ARRAY TO HOLD METRICS
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="1406d-411">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-411">**OUTPUT**</span></span>

<span data-ttu-id="1406d-412">RMSE = 0,906972198262</span><span class="sxs-lookup"><span data-stu-id="1406d-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="1406d-413">Racine carrée = 0,740751197012</span><span class="sxs-lookup"><span data-stu-id="1406d-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="1406d-414">Durée d’exécution de la cellule ci-dessus : 69,17 secondes</span><span class="sxs-lookup"><span data-stu-id="1406d-414">Time taken to execute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="1406d-415">Nettoyer des objets de la mémoire et imprimer les emplacements des modèles</span><span class="sxs-lookup"><span data-stu-id="1406d-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="1406d-416">Utilisez `unpersist()` pour supprimer les objets mis en cache en mémoire.</span><span class="sxs-lookup"><span data-stu-id="1406d-416">Use `unpersist()` to delete objects cached in memory.</span></span>

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


<span data-ttu-id="1406d-417">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-417">**OUTPUT**</span></span>

<span data-ttu-id="1406d-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span><span class="sxs-lookup"><span data-stu-id="1406d-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="1406d-419">** Impression chemin d’accès des fichiers de modèle à utiliser dans le bloc-notes de consommation.</span><span class="sxs-lookup"><span data-stu-id="1406d-419">**Printout path to model files to be used in the consumption notebook.</span></span> <span data-ttu-id="1406d-420">** Pour consommer et le score d’un jeu de données indépendant, vous devez copier et coller ces noms de fichiers dans le bloc-notes « consommation ».</span><span class="sxs-lookup"><span data-stu-id="1406d-420">** To consume and score an independent data-set, you need to copy and paste these file names in the "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="1406d-421">**SORTIE**</span><span class="sxs-lookup"><span data-stu-id="1406d-421">**OUTPUT**</span></span>

<span data-ttu-id="1406d-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="1406d-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="1406d-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="1406d-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="1406d-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="1406d-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="1406d-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="1406d-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="1406d-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="1406d-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="1406d-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="1406d-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="1406d-428">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="1406d-428">What's next?</span></span>
<span data-ttu-id="1406d-429">Maintenant que vous avez créé des modèles de régression et de classification avec la bibliothèque MlLib Spark, vous êtes prêt à apprendre à noter et évaluer ces modèles.</span><span class="sxs-lookup"><span data-stu-id="1406d-429">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span></span>

<span data-ttu-id="1406d-430">**Consommation de modèles :** pour apprendre à noter et évaluer les modèles de classification et de régression créés dans cette rubrique, consultez [Noter et évaluer des modèles Machine Learning intégrés Spark](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="1406d-430">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

