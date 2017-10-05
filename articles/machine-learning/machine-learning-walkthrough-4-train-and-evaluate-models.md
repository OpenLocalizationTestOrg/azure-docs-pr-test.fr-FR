---
title: "Étape 4 : formation et évaluation des modèles d’analyse prédictive | Microsoft Docs"
description: "Étape 4 de la procédure pas à pas du développement d’une solution prédictive : formation, notation et évaluation des multiples modèles dans Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 58d46dd1464ec0a3fc9639f78d4429e0e778c2bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-the-predictive-analytic-models"></a><span data-ttu-id="1b3f1-103">Étape 4 de la procédure pas à pas : formation et évaluation des modèles d’analyse prédictive</span><span class="sxs-lookup"><span data-stu-id="1b3f1-103">Walkthrough Step 4: Train and evaluate the predictive analytic models</span></span>
<span data-ttu-id="1b3f1-104">Cette rubrique décrit la quatrième étape de la procédure pas à pas [Développement d’une solution d’analyse prédictive avec Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="1b3f1-104">This topic contains the fourth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="1b3f1-105">Créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1b3f1-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="1b3f1-106">Télécharger des données existantes</span><span class="sxs-lookup"><span data-stu-id="1b3f1-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="1b3f1-107">Créer une expérience</span><span class="sxs-lookup"><span data-stu-id="1b3f1-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="1b3f1-108">**Former et évaluer les modèles**</span><span class="sxs-lookup"><span data-stu-id="1b3f1-108">**Train and evaluate the models**</span></span>
5. [<span data-ttu-id="1b3f1-109">Déployer le service web</span><span class="sxs-lookup"><span data-stu-id="1b3f1-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="1b3f1-110">Accéder au service web</span><span class="sxs-lookup"><span data-stu-id="1b3f1-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="1b3f1-111">Un des avantages de l’utilisation d’Azure Machine Learning Studio pour créer des modèles d’apprentissage automatique est la possibilité d’essayer simultanément plusieurs types de modèle dans une expérience et de comparer les résultats.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-111">One of the benefits of using Azure Machine Learning Studio for creating machine learning models is the ability to try more than one type of model at a time in a single experiment and compare the results.</span></span> <span data-ttu-id="1b3f1-112">Ce type d’expérimentation vous aide à trouver la meilleure solution à votre problème.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-112">This type of experimentation helps you find the best solution for your problem.</span></span>

<span data-ttu-id="1b3f1-113">Dans l’expérience développée au fil de cette procédure pas à pas, nous allons créer deux types de modèles, puis comparer les résultats d’évaluation afin de choisir l’algorithme que nous utiliserons dans notre expérience finale.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-113">In the experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results to decide which algorithm we want to use in our final experiment.</span></span>  

<span data-ttu-id="1b3f1-114">Nous avons le choix entre différents modèles.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-114">There are various models we could choose from.</span></span> <span data-ttu-id="1b3f1-115">Pour connaître les modèles disponibles, développez le nœud **Machine Learning** dans la palette des modules, puis développez **Initialiser le modèle** et les nœuds inférieurs.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-115">To see the models available, expand the **Machine Learning** node in the module palette, and then expand **Initialize Model** and the nodes beneath it.</span></span> <span data-ttu-id="1b3f1-116">Pour cette expérience, nous allons sélectionner les modules [Machines à vecteurs de support à deux classes][two-class-support-vector-machine] et [Arbres de décision optimisé à deux classes][two-class-boosted-decision-tree].</span><span class="sxs-lookup"><span data-stu-id="1b3f1-116">For the purposes of this experiment, we'll select the [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="1b3f1-117">Pour déterminer facilement l’algorithme Machine Learning le mieux adapté au problème à résoudre, consultez [Comment choisir les algorithmes dans Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="1b3f1-117">To get help deciding which Machine Learning algorithm best suits the particular problem you're trying to solve, see [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-the-models"></a><span data-ttu-id="1b3f1-118">Formation des modèles</span><span class="sxs-lookup"><span data-stu-id="1b3f1-118">Train the models</span></span>

<span data-ttu-id="1b3f1-119">Nous allons ajouter le module [Arbre de décision optimisé à deux classes][two-class-boosted-decision-tree] et le module [Machines à vecteurs de support à deux classes][two-class-support-vector-machine] dans cette expérience.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-119">We'll add both the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="1b3f1-120">Arbre de décision optimisé à deux classes</span><span class="sxs-lookup"><span data-stu-id="1b3f1-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="1b3f1-121">Configurons d’abord le modèle Arbre de décision optimisé.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-121">First, let's set up the boosted decision tree model.</span></span>

1. <span data-ttu-id="1b3f1-122">Recherchez le module [Arbre de décision optimisé à deux classes][two-class-boosted-decision-tree] dans la palette des modules et faites-le glisser sur la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-122">Find the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="1b3f1-123">Recherchez le module [Former le modèle][train-model], faites-le glisser sur la zone de dessin et connectez la sortie du module [Arbre de décision optimisé à deux classes][two-class-boosted-decision-tree] au port d’entrée de gauche du module [Former le modèle][train-model].</span><span class="sxs-lookup"><span data-stu-id="1b3f1-123">Find the [Train Model][train-model] module, drag it onto the canvas, and then connect the output of the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="1b3f1-124">Le module [Arbre de décision optimisé à deux classes][two-class-boosted-decision-tree] initialise le modèle générique, tandis que le module [Former le modèle][train-model] utilise les données d’apprentissage pour former le modèle.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-124">The [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes the generic model, and [Train Model][train-model] uses training data to train the model.</span></span> 

3. <span data-ttu-id="1b3f1-125">Connectez la sortie de gauche du module [Exécuter le script R][execute-r-script] de gauche au port d’entrée de droite du module [Former le modèle][train-model] (à l’[étape 3](machine-learning-walkthrough-3-create-new-experiment.md) de cette procédure, nous avons décidé d’utiliser les données provenant du côté gauche du module Fractionner les données pour la formation).</span><span class="sxs-lookup"><span data-stu-id="1b3f1-125">Connect the left output of the left [Execute R Script][execute-r-script] module to the right input port of the [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough to use the data coming from the left side of the Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="1b3f1-126">Pour cette expérience, nous n’avons pas besoin de deux des entrées et de l’une des sorties du module [Exécuter le script R][execute-r-script]. Nous pouvons donc ne les laisser sans liaison.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-126">We don't need two of the inputs and one of the outputs of the [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="1b3f1-127">Cette partie de l'expérience ressemble alors à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="1b3f1-127">This portion of the experiment now looks something like this:</span></span>  

![Training a model][1]

<span data-ttu-id="1b3f1-129">Maintenant, nous devons indiquer au module [Former le modèle][train-model] que nous voulons utiliser le modèle pour prédire la valeur Risque de crédit.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-129">Now we need to tell the [Train Model][train-model] module that we want the model to predict the Credit Risk value.</span></span>

1. <span data-ttu-id="1b3f1-130">Sélectionnez le module [Former le modèle][train-model].</span><span class="sxs-lookup"><span data-stu-id="1b3f1-130">Select the [Train Model][train-model] module.</span></span> <span data-ttu-id="1b3f1-131">Dans le volet **Propriétés**, cliquez sur **Lancer le sélecteur de colonne**.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-131">In the **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="1b3f1-132">Dans la boîte de dialogue **Sélectionner une seule colonne**, tapez « risque de crédit » dans le champ de recherche sous **Colonnes disponibles**, sélectionnez « Risque de crédit » ci-dessous et cliquez sur la flèche droite (**>**) pour déplacer « Risque de crédit » vers **Colonnes sélectionnées**.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-132">In the **Select a single column** dialog, type "credit risk" in the search field under **Available Columns**, select "Credit risk" below, and click the right arrow button (**>**) to move "Credit risk" to **Selected Columns**.</span></span> 

    ![Sélectionnez la colonne Risque de crédit pour le module Former le modèle][0]

3. <span data-ttu-id="1b3f1-134">Cliquez sur la coche **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-134">Click the **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="1b3f1-135">Machine à vecteurs de support à deux classes</span><span class="sxs-lookup"><span data-stu-id="1b3f1-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="1b3f1-136">Nous configurons ensuite le modèle SVM.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-136">Next, we set up the SVM model.</span></span>  

<span data-ttu-id="1b3f1-137">Tout d’abord, une petite explication sur SVM.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="1b3f1-138">Les arbres de décision optimisés fonctionnent bien avec tout type de caractéristique.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="1b3f1-139">Toutefois, le module SVM générant un classifieur linéaire, le modèle qu'il génère obtient la meilleure erreur de test quand toutes les caractéristiques numériques sont à la même échelle.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-139">However, since the SVM module generates a linear classifier, the model that it generates has the best test error when all numeric features have the same scale.</span></span> <span data-ttu-id="1b3f1-140">Pour convertir toutes les fonctions numériques à la même échelle, nous utilisons une transformation « Tanh » (avec le module [Normaliser les données][normalize-data]).</span><span class="sxs-lookup"><span data-stu-id="1b3f1-140">To convert all numeric features to the same scale, we use a "Tanh" transformation (with the [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="1b3f1-141">Cette opération transforme les nombres en plage [0,1].</span><span class="sxs-lookup"><span data-stu-id="1b3f1-141">This transforms our numbers into the [0,1] range.</span></span> <span data-ttu-id="1b3f1-142">Le module SVM convertit les fonctions de chaîne en fonctions catégorielles, puis en fonctions 0/1 binaires. Il est donc inutile de les transformer manuellement.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-142">The SVM module converts string features to categorical features and then to binary 0/1 features, so we don't need to manually transform string features.</span></span> <span data-ttu-id="1b3f1-143">De même, nous ne voulons pas transformer la colonne Risque du crédit (colonne 21). Elle est numérique et contient la valeur que nous apprenons à prédire au modèle ; nous devons donc la laisser seule.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-143">Also, we don't want to transform the Credit Risk column (column 21) - it's numeric, but it's the value we're training the model to predict, so we need to leave it alone.</span></span>  

<span data-ttu-id="1b3f1-144">Pour configurer le modèle SVM, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1b3f1-144">To set up the SVM model, do the following:</span></span>

1. <span data-ttu-id="1b3f1-145">Recherchez le module [Machine à vecteurs de support à deux classes][two-class-support-vector-machine] dans la palette des modules et faites-le glisser sur la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-145">Find the [Two-Class Support Vector Machine][two-class-support-vector-machine] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="1b3f1-146">Cliquez avec le bouton droit sur le module [Former le modèle][train-model], sélectionnez **Copier**, puis cliquez avec le bouton droit sur la zone de dessin et sélectionnez **Coller**.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-146">Right-click the [Train Model][train-model] module, select **Copy**, and then right-click the canvas and select **Paste**.</span></span> <span data-ttu-id="1b3f1-147">La copie du module [Former le modèle][train-model] contient les mêmes colonnes que l’original.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-147">The copy of the [Train Model][train-model] module has the same column selection as the original.</span></span>

3. <span data-ttu-id="1b3f1-148">Connectez la sortie du module [Machines à vecteurs de support à deux classes][two-class-support-vector-machine] au port d’entrée de gauche du second module [Former le modèle][train-model].</span><span class="sxs-lookup"><span data-stu-id="1b3f1-148">Connect the output of the [Two-Class Support Vector Machine][two-class-support-vector-machine] module to the left input port of the second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="1b3f1-149">Trouvez le module [Normaliser les données][normalize-data] et faites-le glisser vers la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-149">Find the [Normalize Data][normalize-data] module and drag it onto the canvas.</span></span>

5. <span data-ttu-id="1b3f1-150">Connectez la sortie de gauche du module [Exécuter le script R][execute-r-script] de gauche à l’entrée de ce module (notez que le port de sortie d’un module peut être connecté à plusieurs autres modules).</span><span class="sxs-lookup"><span data-stu-id="1b3f1-150">Connect the left output of the left [Execute R Script][execute-r-script] module to the input of this module (notice that the output port of a module may be connected to more than one other module).</span></span>

6. <span data-ttu-id="1b3f1-151">Connectez le port de sortie de gauche du module [Normaliser les données][normalize-data] au port d’entrée de droite du deuxième module [Former le modèle][train-model].</span><span class="sxs-lookup"><span data-stu-id="1b3f1-151">Connect the left output port of the [Normalize Data][normalize-data] module to the right input port of the second [Train Model][train-model] module.</span></span>

<span data-ttu-id="1b3f1-152">Cette partie de l'expérience ressemble alors à ceci :</span><span class="sxs-lookup"><span data-stu-id="1b3f1-152">This portion of our experiment should now look something like this:</span></span>  

![Training the second model][2]  

<span data-ttu-id="1b3f1-154">Configurez maintenant le module [Normaliser les données][normalize-data] :</span><span class="sxs-lookup"><span data-stu-id="1b3f1-154">Now configure the [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="1b3f1-155">Cliquez pour sélectionner le module [Normaliser les données][normalize-data].</span><span class="sxs-lookup"><span data-stu-id="1b3f1-155">Click to select the [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="1b3f1-156">Dans le volet **Propriétés**, sélectionnez **Tanh** comme paramètre de la **Méthode de transformation**.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-156">In the **Properties** pane, select **Tanh** for the **Transformation method** parameter.</span></span>

2. <span data-ttu-id="1b3f1-157">Cliquez sur **Lancer le sélecteur de colonne**, sélectionnez « Aucune colonne » pour **Commencer par**, sélectionnez **Inclure** dans la première liste déroulante, **Type de colonne** dans la deuxième, puis **Numérique** dans la troisième.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in the first dropdown, select **column type** in the second dropdown, and select **Numeric** in the third dropdown.</span></span> <span data-ttu-id="1b3f1-158">Cette action spécifie que toutes les colonnes numériques (et elles seules) sont transformées.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-158">This specifies that all the numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="1b3f1-159">Cliquez sur le signe plus (+) à droite de cette ligne. Cette opération crée une ligne de listes déroulantes.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-159">Click the plus sign (+) to the right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="1b3f1-160">Sélectionnez **Exclure** dans la première liste déroulante, sélectionnez des **noms de colonne** dans la deuxième liste déroulante et entrez « Risque de crédit » dans le champ textuel.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-160">Select **Exclude** in the first dropdown, select **column names** in the second dropdown, and enter "Credit risk" in the text field.</span></span> <span data-ttu-id="1b3f1-161">Cette opération indique que la colonne Risque de crédit doit être ignorée (en effet, celle-ci étant numérique, elle serait transformée).</span><span class="sxs-lookup"><span data-stu-id="1b3f1-161">This specifies that the Credit Risk column should be ignored (we need to do this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="1b3f1-162">Cliquez sur la coche **OK**.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-162">Click the **OK** check mark.</span></span>  

    ![Sélectionner des colonnes pour le module Normaliser les données][5]

<span data-ttu-id="1b3f1-164">Le module [Normaliser les données][normalize-data] est maintenant configuré pour effectuer une transformation Tanh sur toutes les colonnes numériques, à l’exception de la colonne Risque de crédit.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-164">The [Normalize Data][normalize-data] module is now set to perform a Tanh transformation on all numeric columns except for the Credit Risk column.</span></span>  

## <a name="score-and-evaluate-the-models"></a><span data-ttu-id="1b3f1-165">Notation et évaluation des modèles</span><span class="sxs-lookup"><span data-stu-id="1b3f1-165">Score and evaluate the models</span></span>

<span data-ttu-id="1b3f1-166">Nous utilisons les données de test exclues par le module [Fractionner les données][split] pour noter nos modèles formés.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-166">We use the testing data that was separated out by the [Split Data][split] module to score our trained models.</span></span> <span data-ttu-id="1b3f1-167">Nous pouvons ensuite comparer les résultats des deux modèles pour savoir lequel donne les meilleurs résultats.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-167">We can then compare the results of the two models to see which generated better results.</span></span>  

### <a name="add-the-score-model-modules"></a><span data-ttu-id="1b3f1-168">Ajouter les modules Noter le modèle</span><span class="sxs-lookup"><span data-stu-id="1b3f1-168">Add the Score Model modules</span></span>

1. <span data-ttu-id="1b3f1-169">Recherchez le module [Noter le modèle][score-model] et faites-le glisser sur la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-169">Find the [Score Model][score-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="1b3f1-170">Connectez le module [Former le modèle][train-model] relié au module [Arbre de décision optimisé à deux classes][two-class-boosted-decision-tree], au port d’entrée de gauche du module [Noter le modèle][score-model].</span><span class="sxs-lookup"><span data-stu-id="1b3f1-170">Connect the [Train Model][train-model] module that's connected to the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="1b3f1-171">Connectez le module [Exécuter le script R][execute-r-script] (nos données de test) au port d’entrée de droite du module [Noter le modèle][score-model].</span><span class="sxs-lookup"><span data-stu-id="1b3f1-171">Connect the right [Execute R Script][execute-r-script] module (our testing data) to the right input port of the [Score Model][score-model] module.</span></span>

    ![Module Noter le modèle connecté][6]
   
   <span data-ttu-id="1b3f1-173">Le module [Noter le modèle][score-model] peut maintenant récupérer les informations sur le crédit dans les données de test, les traiter à l’aide du modèle et comparer les prévisions générées par le modèle à la colonne Risque de crédit dans les données de test.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-173">The [Score Model][score-model] module can now take the credit information from the testing data, run it through the model, and compare the predictions the model generates with the actual credit risk column in the testing data.</span></span>

4. <span data-ttu-id="1b3f1-174">Copiez et collez le module [Noter le modèle][score-model] pour créer une deuxième copie.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-174">Copy and paste the [Score Model][score-model] module to create a second copy.</span></span>

5. <span data-ttu-id="1b3f1-175">Connectez la sortie du modèle SVM (c’est-à-dire le port de sortie du module [Former le modèle][train-model] relié au module [Arbre de décision optimisé à deux classes][two-class-support-vector-machine]) au port d’entrée du deuxième module [Noter le modèle][score-model].</span><span class="sxs-lookup"><span data-stu-id="1b3f1-175">Connect the output of the SVM model (that is, the output port of the [Train Model][train-model] module that's connected to the [Two-Class Support Vector Machine][two-class-support-vector-machine] module) to the input port of the second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="1b3f1-176">Pour le modèle SVM, nous devons effectuer la même transformation pour tester les données comme nous l’avons fait pour les données de formation.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-176">For the SVM model, we have to do the same transformation to the test data as we did to the training data.</span></span> <span data-ttu-id="1b3f1-177">Donc, copiez et collez le module [Normaliser les données][normalize-data] pour créer une autre copie et connectez-la au module [Exécuter le script R][execute-r-script] de droite.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-177">So copy and paste the [Normalize Data][normalize-data] module to create a second copy and connect it to the right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="1b3f1-178">Connectez la sortie de gauche du deuxième module [Noter le modèle][normalize-data] au port d’entrée de droite du deuxième module [Noter le modèle][score-model].</span><span class="sxs-lookup"><span data-stu-id="1b3f1-178">Connect the left output of the second [Normalize Data][normalize-data] module to the right input port of the second [Score Model][score-model] module.</span></span>

    ![Deux modules Noter le modèle connectés][7]

### <a name="add-the-evaluate-model-module"></a><span data-ttu-id="1b3f1-180">Ajouter le module Évaluer le modèle</span><span class="sxs-lookup"><span data-stu-id="1b3f1-180">Add the Evaluate Model module</span></span>

<span data-ttu-id="1b3f1-181">Pour évaluer les deux résultats et les comparer, nous utilisons un module [Évaluer le modèle][evaluate-model].</span><span class="sxs-lookup"><span data-stu-id="1b3f1-181">To evaluate the two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="1b3f1-182">Recherchez le module [Évaluer le modèle][evaluate-model] et faites-le glisser vers la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-182">Find the [Evaluate Model][evaluate-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="1b3f1-183">Connectez le port de sortie du module [Noter le modèle][score-model] associé au modèle Arbre de décision optimisé, au port d’entrée gauche du module [Évaluer le modèle][evaluate-model].</span><span class="sxs-lookup"><span data-stu-id="1b3f1-183">Connect the output port of the [Score Model][score-model] module associated with the boosted decision tree model to the left input port of the [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="1b3f1-184">Connectez l’autre module [Noter le modèle][score-model] au port d’entrée de droite.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-184">Connect the other [Score Model][score-model] module to the right input port.</span></span>  

    ![Module Évaluer le modèle connecté][8]

### <a name="run-the-experiment-and-check-the-results"></a><span data-ttu-id="1b3f1-186">Exécuter l’expérience et vérifier les résultats</span><span class="sxs-lookup"><span data-stu-id="1b3f1-186">Run the experiment and check the results</span></span>

<span data-ttu-id="1b3f1-187">Pour exécuter l’expérience, cliquez sur le bouton **EXÉCUTER** sous le canevas.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-187">To run the experiment, click the **RUN** button below the canvas.</span></span> <span data-ttu-id="1b3f1-188">Cette opération peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-188">It may take a few minutes.</span></span> <span data-ttu-id="1b3f1-189">Un indicateur rotatif sur chaque module indique que l’exécution est en cours. Puis une coche verte s’affiche pour signaler que l’exécution du module est terminée.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when the module is finished.</span></span> <span data-ttu-id="1b3f1-190">Lorsque tous les modules comportent une coche, l'exécution de l'expérience est terminée.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-190">When all the modules have a check mark, the experiment has finished running.</span></span>

<span data-ttu-id="1b3f1-191">L'expérience doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="1b3f1-191">The experiment should now look something like this:</span></span>  

![Evaluating both models][3]

<span data-ttu-id="1b3f1-193">Pour vérifier les résultats, cliquez sur le port de sortie du module [Évaluer le modèle][evaluate-model] et sélectionnez **Visualiser**.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-193">To check the results, click the output port of the [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="1b3f1-194">Le module [Évaluer le modèle][evaluate-model] produit une paire de courbes et de mesures qui vous permettent de comparer les résultats des deux modèles notés.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-194">The [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you to compare the results of the two scored models.</span></span> <span data-ttu-id="1b3f1-195">Vous pouvez afficher les résultats sous forme de courbes Receiver Operator Characteristic (ROC), Precision/Recall ou Lift.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-195">You can view the results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="1b3f1-196">Les données supplémentaires affichées comprennent une matrice de confusion, les valeurs cumulées pour l’aire sous la courbe (ASC) et d’autres mesures.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-196">Additional data displayed includes a confusion matrix, cumulative values for the area under the curve (AUC), and other metrics.</span></span> <span data-ttu-id="1b3f1-197">Vous pouvez modifier la valeur du seuil en déplaçant le curseur vers la gauche ou la droite et voir son influence sur l'ensemble des mesures.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-197">You can change the threshold value by moving the slider left or right and see how it affects the set of metrics.</span></span>  

<span data-ttu-id="1b3f1-198">À droite du graphique, cliquez sur **Jeu de données noté** ou **Jeu de données noté à comparer** pour mettre en surbrillance la courbe associée et afficher les mesures associées en dessous.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-198">To the right of the graph, click **Scored dataset** or **Scored dataset to compare** to highlight the associated curve and to display the associated metrics below.</span></span> <span data-ttu-id="1b3f1-199">Dans la légende des courbes, « Jeu de données noté » correspond au port d’entrée de gauche du module [Évaluer le modèle][evaluate-model] (en l’occurrence, le modèle Arbre de décision optimisé).</span><span class="sxs-lookup"><span data-stu-id="1b3f1-199">In the legend for the curves, "Scored dataset" corresponds to the left input port of the [Evaluate Model][evaluate-model] module - in our case, this is the boosted decision tree model.</span></span> <span data-ttu-id="1b3f1-200">« Jeu de données noté à comparer » correspond au port d’entrée de droite, le modèle SVM dans notre cas.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-200">"Scored dataset to compare" corresponds to the right input port - the SVM model in our case.</span></span> <span data-ttu-id="1b3f1-201">Lorsque vous cliquez sur une de ces étiquettes, la courbe de ce modèle apparaît en surbrillance ainsi que les mesures correspondantes, comme dans le graphique suivant.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-201">When you click one of these labels, the curve for that model is highlighted and the corresponding metrics are displayed, as shown in the following graphic.</span></span>  

![ROC curves for models][4]

<span data-ttu-id="1b3f1-203">En examinant ces valeurs, vous pouvez déterminer quel modèle est le plus susceptible de fournir les résultats que vous recherchez.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-203">By examining these values, you can decide which model is closest to giving you the results you're looking for.</span></span> <span data-ttu-id="1b3f1-204">Vous pouvez revenir en arrière et relancer votre expérience en modifiant les valeurs des différents modèles.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-204">You can go back and iterate on your experiment by changing parameter values in the different models.</span></span> 

<span data-ttu-id="1b3f1-205">Cette procédure n’explique pas comment interpréter ces résultats et optimiser les performances du modèle.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-205">The science and art of interpreting these results and tuning the model performance is outside the scope of this walkthrough.</span></span> <span data-ttu-id="1b3f1-206">Pour en savoir plus, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="1b3f1-206">For additional help, you might read the following articles:</span></span>
- [<span data-ttu-id="1b3f1-207">Évaluation des performances d’un modèle dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1b3f1-207">How to evaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="1b3f1-208">Sélection des paramètres permettant d’optimiser des algorithmes dans Microsoft Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1b3f1-208">Choose parameters to optimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="1b3f1-209">Interprétation des résultats de modèle dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1b3f1-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="1b3f1-210">À chaque exécution de l’expérience, un enregistrement de cet essai est conservé dans l’historique d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-210">Each time you run the experiment a record of that iteration is kept in the Run History.</span></span> <span data-ttu-id="1b3f1-211">Vous pouvez afficher tous les essais de votre expérience (et y revenir) en cliquant sur **AFFICHER L'HISTORIQUE D'EXÉCUTION** , sous le canevas.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-211">You can view these iterations, and return to any of them, by clicking **VIEW RUN HISTORY** below the canvas.</span></span> <span data-ttu-id="1b3f1-212">Vous pouvez également cliquer sur **Exécution précédente** dans le volet **Propriétés** pour revenir à l’exécution précédant immédiatement celle que vous avez ouverte.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-212">You can also click **Prior Run** in the **Properties** pane to return to the iteration immediately preceding the one you have open.</span></span>
> 
> <span data-ttu-id="1b3f1-213">Vous pouvez faire une copie d’un essai de votre expérience en cliquant sur **ENREGISTRER SOUS** sous le canevas.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below the canvas.</span></span> 
> <span data-ttu-id="1b3f1-214">Utilisez les propriétés **Résumé** et **Description** de l’expérience pour conserver un enregistrement de vos essais dans les itérations de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="1b3f1-214">Use the experiment's **Summary** and **Description** properties to keep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="1b3f1-215">Pour en savoir plus, consultez la section [Gérer les itérations des expériences dans Microsoft Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="1b3f1-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="1b3f1-216"> **: [Déployer le service web](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="1b3f1-216">**Next: [Deploy the web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: ./media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
