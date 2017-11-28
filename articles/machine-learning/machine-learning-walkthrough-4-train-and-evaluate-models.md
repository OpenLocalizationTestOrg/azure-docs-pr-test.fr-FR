---
title: "Étape 4 : Effectuer l’apprentissage et évaluer des modèles d’analyse prédictive hello | Documents Microsoft"
description: "Étape 4 Hello développer la procédure pas à pas une solution prédictive : effectuer l’apprentissage, évaluer et évaluer plusieurs modèles dans Azure Machine Learning Studio."
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
ms.openlocfilehash: d86d7c5ae7524f71fe44d985db67c4618b7965a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-4-train-and-evaluate-hello-predictive-analytic-models"></a><span data-ttu-id="c4db9-103">Procédure pas à pas, étape 4 : Effectuer l’apprentissage et évaluer des modèles d’analyse prédictive hello</span><span class="sxs-lookup"><span data-stu-id="c4db9-103">Walkthrough Step 4: Train and evaluate hello predictive analytic models</span></span>
<span data-ttu-id="c4db9-104">Cette rubrique contient hello quatrième étape d’hello procédure pas à pas, [développer une solution prédictive analytique dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="c4db9-104">This topic contains hello fourth step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="c4db9-105">Créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c4db9-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="c4db9-106">Télécharger des données existantes</span><span class="sxs-lookup"><span data-stu-id="c4db9-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="c4db9-107">Créer une expérience</span><span class="sxs-lookup"><span data-stu-id="c4db9-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="c4db9-108">**L’apprentissage et évaluer des modèles de hello**</span><span class="sxs-lookup"><span data-stu-id="c4db9-108">**Train and evaluate hello models**</span></span>
5. [<span data-ttu-id="c4db9-109">Déployer le service Web de hello</span><span class="sxs-lookup"><span data-stu-id="c4db9-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="c4db9-110">Accéder au service Web de hello</span><span class="sxs-lookup"><span data-stu-id="c4db9-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="c4db9-111">Un des avantages de hello de l’utilisation d’Azure Machine Learning Studio pour la création de modèles d’apprentissage automatique est hello capacité tootry plus d’un type de modèle à la fois dans une expérience unique et comparer les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-111">One of hello benefits of using Azure Machine Learning Studio for creating machine learning models is hello ability tootry more than one type of model at a time in a single experiment and compare hello results.</span></span> <span data-ttu-id="c4db9-112">Ce type d’expérimentation vous aide à trouver des hello meilleure solution pour votre problème.</span><span class="sxs-lookup"><span data-stu-id="c4db9-112">This type of experimentation helps you find hello best solution for your problem.</span></span>

<span data-ttu-id="c4db9-113">Dans l’expérience hello nous développons dans cette procédure pas à pas, nous créer deux différents types de modèles et ensuite comparer leur toodecide résultats score algorithme nous souhaitons toouse dans notre expérience finale.</span><span class="sxs-lookup"><span data-stu-id="c4db9-113">In hello experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results toodecide which algorithm we want toouse in our final experiment.</span></span>  

<span data-ttu-id="c4db9-114">Nous avons le choix entre différents modèles.</span><span class="sxs-lookup"><span data-stu-id="c4db9-114">There are various models we could choose from.</span></span> <span data-ttu-id="c4db9-115">modèles de hello toosee disponibles, développez hello **Machine Learning** nœud dans la palette de module hello, puis développez **initialiser le modèle** et nœuds hello situé sous celui-ci.</span><span class="sxs-lookup"><span data-stu-id="c4db9-115">toosee hello models available, expand hello **Machine Learning** node in hello module palette, and then expand **Initialize Model** and hello nodes beneath it.</span></span> <span data-ttu-id="c4db9-116">Fins hello de cette expérience, nous allons sélectionner hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] (SVM) et hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] modules.</span><span class="sxs-lookup"><span data-stu-id="c4db9-116">For hello purposes of this experiment, we'll select hello [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="c4db9-117">tooget déterminer plus facilement l’algorithme d’apprentissage mieux adapté à la problématique en particulier hello que vous essayez de toosolve, consultez [comment toochoose des algorithmes pour Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="c4db9-117">tooget help deciding which Machine Learning algorithm best suits hello particular problem you're trying toosolve, see [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-hello-models"></a><span data-ttu-id="c4db9-118">L’apprentissage des modèles de hello</span><span class="sxs-lookup"><span data-stu-id="c4db9-118">Train hello models</span></span>

<span data-ttu-id="c4db9-119">Nous allons ajouter deux hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module et [Two-Class Support Vector Machine] [ two-class-support-vector-machine] ce module Faites des essais.</span><span class="sxs-lookup"><span data-stu-id="c4db9-119">We'll add both hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="c4db9-120">Arbre de décision optimisé à deux classes</span><span class="sxs-lookup"><span data-stu-id="c4db9-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="c4db9-121">Tout d’abord, nous allons définir modèle d’arbre de décision augmenté de hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-121">First, let's set up hello boosted decision tree model.</span></span>

1. <span data-ttu-id="c4db9-122">Recherche hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module dans la palette de module hello et faites-le glisser sur le canevas de hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-122">Find hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="c4db9-123">Recherche hello [Train Model] [ train-model] module, faites glisser sur la zone de dessin hello et connectez-vous sortie hello Hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree]module toohello gauche d’un port d’entrée de hello [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="c4db9-123">Find hello [Train Model][train-model] module, drag it onto hello canvas, and then connect hello output of hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="c4db9-124">Hello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] module initialise modèle générique hello et [Train Model] [ train-model] utilise les données d’apprentissage modèle de hello tootrain.</span><span class="sxs-lookup"><span data-stu-id="c4db9-124">hello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes hello generic model, and [Train Model][train-model] uses training data tootrain hello model.</span></span> 

3. <span data-ttu-id="c4db9-125">Connecter la sortie de gauche hello de hello à gauche [Execute R Script] [ execute-r-script] toohello module droit d’entrée de port de hello [Train Model] [ train-model] module (nous décidé dans [étape 3](machine-learning-walkthrough-3-create-new-experiment.md) de cette procédure pas à pas toouse hello les données provenant hello gauche hello fractionnement du module de données pour l’apprentissage).</span><span class="sxs-lookup"><span data-stu-id="c4db9-125">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello right input port of hello [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough toouse hello data coming from hello left side of hello Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="c4db9-126">Nous n’avez pas besoin de deux entrées de hello et une des sorties hello Hello [Execute R Script] [ execute-r-script] module pour cette expérience, donc nous pouvons les laisser détachés.</span><span class="sxs-lookup"><span data-stu-id="c4db9-126">We don't need two of hello inputs and one of hello outputs of hello [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="c4db9-127">Cette partie de l’expérience de hello ressemble maintenant à ceci :</span><span class="sxs-lookup"><span data-stu-id="c4db9-127">This portion of hello experiment now looks something like this:</span></span>  

![Training a model][1]

<span data-ttu-id="c4db9-129">Maintenant nous devons tootell hello [Train Model] [ train-model] module que nous souhaitons valeur risque de crédit de hello modèle toopredict hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-129">Now we need tootell hello [Train Model][train-model] module that we want hello model toopredict hello Credit Risk value.</span></span>

1. <span data-ttu-id="c4db9-130">Sélectionnez hello [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="c4db9-130">Select hello [Train Model][train-model] module.</span></span> <span data-ttu-id="c4db9-131">Bonjour **propriétés** volet, cliquez sur **sélecteur de colonne lancement**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-131">In hello **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="c4db9-132">Bonjour **sélectionner une seule colonne** boîte de dialogue, tapez « risque de crédit » dans le champ de recherche hello sous **colonnes disponibles**, sélectionnez « Risque de crédit » ci-dessous et cliquez sur le bouton de flèche droite hello ( **>** ) toomove « Risque de crédit « trop**colonnes sélectionnées**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-132">In hello **Select a single column** dialog, type "credit risk" in hello search field under **Available Columns**, select "Credit risk" below, and click hello right arrow button (**>**) toomove "Credit risk" too**Selected Columns**.</span></span> 

    ![Sélectionnez colonne de risque de crédit hello pour le module de Train Model hello][0]

3. <span data-ttu-id="c4db9-134">Cliquez sur hello **OK** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="c4db9-134">Click hello **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="c4db9-135">Machine à vecteurs de support à deux classes</span><span class="sxs-lookup"><span data-stu-id="c4db9-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="c4db9-136">Ensuite, nous configurons modèle SVM de hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-136">Next, we set up hello SVM model.</span></span>  

<span data-ttu-id="c4db9-137">Tout d’abord, une petite explication sur SVM.</span><span class="sxs-lookup"><span data-stu-id="c4db9-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="c4db9-138">Les arbres de décision optimisés fonctionnent bien avec tout type de caractéristique.</span><span class="sxs-lookup"><span data-stu-id="c4db9-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="c4db9-139">Toutefois, étant donné que le module SVM hello génère un classifieur linéaire, modèle hello qu’elle génère a erreur de test meilleures hello lorsque toutes les fonctions numériques ont hello même échelle.</span><span class="sxs-lookup"><span data-stu-id="c4db9-139">However, since hello SVM module generates a linear classifier, hello model that it generates has hello best test error when all numeric features have hello same scale.</span></span> <span data-ttu-id="c4db9-140">tooconvert numérique toutes les fonctionnalités toohello identique à l’échelle, nous utilisons une transformation « Tanh » (avec hello [Normalize Data] [ normalize-data] module).</span><span class="sxs-lookup"><span data-stu-id="c4db9-140">tooconvert all numeric features toohello same scale, we use a "Tanh" transformation (with hello [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="c4db9-141">Cela transforme les numéros de plage de hello [0,1].</span><span class="sxs-lookup"><span data-stu-id="c4db9-141">This transforms our numbers into hello [0,1] range.</span></span> <span data-ttu-id="c4db9-142">module SVM Hello convertit les fonctions toocategorical fonctions de chaîne et des fonctionnalités toobinary 0/1, donc nous ne devez toomanually transformer des fonctions de chaîne.</span><span class="sxs-lookup"><span data-stu-id="c4db9-142">hello SVM module converts string features toocategorical features and then toobinary 0/1 features, so we don't need toomanually transform string features.</span></span> <span data-ttu-id="c4db9-143">En outre, nous ne voulons pas tootransform hello risque de crédit colonne (21) : il est numérique, mais il est valeur hello nous mettons formation hello toopredict de modèle, donc vous devez tooleave elle seule.</span><span class="sxs-lookup"><span data-stu-id="c4db9-143">Also, we don't want tootransform hello Credit Risk column (column 21) - it's numeric, but it's hello value we're training hello model toopredict, so we need tooleave it alone.</span></span>  

<span data-ttu-id="c4db9-144">tooset modèle SVM de hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="c4db9-144">tooset up hello SVM model, do hello following:</span></span>

1. <span data-ttu-id="c4db9-145">Recherche hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] module dans la palette de module hello et faites-le glisser sur le canevas de hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-145">Find hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module in hello module palette and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="c4db9-146">Avec le bouton hello [Train Model] [ train-model] module, sélectionnez **copie**, puis cliquez sur la zone de dessin hello et sélectionnez **coller**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-146">Right-click hello [Train Model][train-model] module, select **Copy**, and then right-click hello canvas and select **Paste**.</span></span> <span data-ttu-id="c4db9-147">Hello copie Hello [Train Model] [ train-model] module a hello sélection de la même colonne en tant que hello d’origine.</span><span class="sxs-lookup"><span data-stu-id="c4db9-147">hello copy of hello [Train Model][train-model] module has hello same column selection as hello original.</span></span>

3. <span data-ttu-id="c4db9-148">Connectez la sortie hello Hello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] toohello du module reste un port d’entrée de hello deuxième [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="c4db9-148">Connect hello output of hello [Two-Class Support Vector Machine][two-class-support-vector-machine] module toohello left input port of hello second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="c4db9-149">Recherche hello [Normalize Data] [ normalize-data] module et faites-le glisser sur le canevas de hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-149">Find hello [Normalize Data][normalize-data] module and drag it onto hello canvas.</span></span>

5. <span data-ttu-id="c4db9-150">Connecter la sortie de gauche hello de hello à gauche [Execute R Script] [ execute-r-script] entrée toohello de module de ce module (Notez que le port de sortie hello d’un module peut être toomore connecté à un autre module).</span><span class="sxs-lookup"><span data-stu-id="c4db9-150">Connect hello left output of hello left [Execute R Script][execute-r-script] module toohello input of this module (notice that hello output port of a module may be connected toomore than one other module).</span></span>

6. <span data-ttu-id="c4db9-151">Se connecter hello gauche du port de sortie de hello [normaliser des données] [ normalize-data] toohello module droite port d’entrée de hello deuxième [Train Model] [ train-model] module.</span><span class="sxs-lookup"><span data-stu-id="c4db9-151">Connect hello left output port of hello [Normalize Data][normalize-data] module toohello right input port of hello second [Train Model][train-model] module.</span></span>

<span data-ttu-id="c4db9-152">Cette partie de l'expérience ressemble alors à ceci :</span><span class="sxs-lookup"><span data-stu-id="c4db9-152">This portion of our experiment should now look something like this:</span></span>  

![Modèle de formation hello deuxième][2]  

<span data-ttu-id="c4db9-154">À présent configurer hello [Normalize Data] [ normalize-data] module :</span><span class="sxs-lookup"><span data-stu-id="c4db9-154">Now configure hello [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="c4db9-155">Cliquez sur tooselect hello [Normalize Data] [ normalize-data] module.</span><span class="sxs-lookup"><span data-stu-id="c4db9-155">Click tooselect hello [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="c4db9-156">Bonjour **propriétés** volet, sélectionnez **Tanh** pour hello **méthode de Transformation** paramètre.</span><span class="sxs-lookup"><span data-stu-id="c4db9-156">In hello **Properties** pane, select **Tanh** for hello **Transformation method** parameter.</span></span>

2. <span data-ttu-id="c4db9-157">Cliquez sur **sélecteur de colonne lancement**, ne sélectionnez « Aucuns colonnes » pour **commencer avec**, sélectionnez **Include** dans hello premier menu déroulant, sélectionnez **le type de colonne**dans hello le deuxième menu déroulant, puis sélectionnez **numérique** dans la liste déroulante de tiers hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in hello first dropdown, select **column type** in hello second dropdown, and select **Numeric** in hello third dropdown.</span></span> <span data-ttu-id="c4db9-158">Spécifie que toutes les colonnes numériques hello (et numériques uniquement) sont transformés.</span><span class="sxs-lookup"><span data-stu-id="c4db9-158">This specifies that all hello numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="c4db9-159">Cliquez sur hello toohello le signe plus (+) à droite de cette ligne, cette opération crée une rangée de menus déroulants.</span><span class="sxs-lookup"><span data-stu-id="c4db9-159">Click hello plus sign (+) toohello right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="c4db9-160">Sélectionnez **exclure** dans hello premier menu déroulant, sélectionnez **les noms de colonne** dans hello la deuxième liste déroulante et entrez « Risque de crédit » dans le champ de texte hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-160">Select **Exclude** in hello first dropdown, select **column names** in hello second dropdown, and enter "Credit risk" in hello text field.</span></span> <span data-ttu-id="c4db9-161">Cela spécifie que cette colonne de risque de crédit hello doit être ignorée (nous devons toodo cela, car cette colonne est numérique et il sera transformé si nous n’avez pas l’exclure).</span><span class="sxs-lookup"><span data-stu-id="c4db9-161">This specifies that hello Credit Risk column should be ignored (we need toodo this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="c4db9-162">Cliquez sur hello **OK** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="c4db9-162">Click hello **OK** check mark.</span></span>  

    ![Sélectionnez des colonnes pour le module de normaliser les données hello][5]

<span data-ttu-id="c4db9-164">Hello [Normalize Data] [ normalize-data] module est désormais ensemble tooperform une transformation Tanh sur toutes les colonnes numériques à l’exception de hello risque de crédit.</span><span class="sxs-lookup"><span data-stu-id="c4db9-164">hello [Normalize Data][normalize-data] module is now set tooperform a Tanh transformation on all numeric columns except for hello Credit Risk column.</span></span>  

## <a name="score-and-evaluate-hello-models"></a><span data-ttu-id="c4db9-165">Calcul du score et évaluer des modèles de hello</span><span class="sxs-lookup"><span data-stu-id="c4db9-165">Score and evaluate hello models</span></span>

<span data-ttu-id="c4db9-166">Nous utilisons hello test des données qui a été séparées par hello [données fractionnées] [ split] module tooscore nos modèles formés.</span><span class="sxs-lookup"><span data-stu-id="c4db9-166">We use hello testing data that was separated out by hello [Split Data][split] module tooscore our trained models.</span></span> <span data-ttu-id="c4db9-167">Nous pouvons ensuite comparer les résultats hello de hello deux modèles toosee qui a généré les meilleurs résultats.</span><span class="sxs-lookup"><span data-stu-id="c4db9-167">We can then compare hello results of hello two models toosee which generated better results.</span></span>  

### <a name="add-hello-score-model-modules"></a><span data-ttu-id="c4db9-168">Ajouter des modules de Score Model hello</span><span class="sxs-lookup"><span data-stu-id="c4db9-168">Add hello Score Model modules</span></span>

1. <span data-ttu-id="c4db9-169">Recherche hello [Score Model] [ score-model] module et faites-le glisser sur le canevas de hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-169">Find hello [Score Model][score-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="c4db9-170">Se connecter hello [Train Model] [ train-model] module qui s’est connecté toohello [Two-Class Boosted Decision Tree] [ two-class-boosted-decision-tree] entrée gauche toohello de module port de hello [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="c4db9-170">Connect hello [Train Model][train-model] module that's connected toohello [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module toohello left input port of hello [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="c4db9-171">Se connecter à droite de hello [Execute R Script] [ execute-r-script] toohello de module (nos données de test) à droite d’entrée de port de hello [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="c4db9-171">Connect hello right [Execute R Script][execute-r-script] module (our testing data) toohello right input port of hello [Score Model][score-model] module.</span></span>

    ![Module Noter le modèle connecté][6]
   
   <span data-ttu-id="c4db9-173">Hello [Score Model] [ score-model] module peut désormais tirer des informations relatives au crédit hello de hello données, exécutez-le jusqu’au modèle hello, de test et des prédictions hello de comparer les modèle hello génère par hello réel risque de crédit colonne Bonjour de données de test.</span><span class="sxs-lookup"><span data-stu-id="c4db9-173">hello [Score Model][score-model] module can now take hello credit information from hello testing data, run it through hello model, and compare hello predictions hello model generates with hello actual credit risk column in hello testing data.</span></span>

4. <span data-ttu-id="c4db9-174">Copiez et collez hello [Score Model] [ score-model] module toocreate une seconde copie.</span><span class="sxs-lookup"><span data-stu-id="c4db9-174">Copy and paste hello [Score Model][score-model] module toocreate a second copy.</span></span>

5. <span data-ttu-id="c4db9-175">Connecter la sortie hello du modèle SVM hello (autrement dit, hello sortie de hello [Train Model] [ train-model] module qui s’est connecté toohello [Two-Class Support Vector Machine] [ two-class-support-vector-machine] module) toohello port d’entrée de hello deuxième [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="c4db9-175">Connect hello output of hello SVM model (that is, hello output port of hello [Train Model][train-model] module that's connected toohello [Two-Class Support Vector Machine][two-class-support-vector-machine] module) toohello input port of hello second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="c4db9-176">Pour un modèle SVM de hello, nous avons toodo hello les mêmes données de test toohello transformation comme nous l’avons fait des données d’apprentissage toohello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-176">For hello SVM model, we have toodo hello same transformation toohello test data as we did toohello training data.</span></span> <span data-ttu-id="c4db9-177">Par conséquent, copiez et collez hello [normaliser les données] [ normalize-data] module toocreate une deuxième copie et le connecter à droite de toohello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="c4db9-177">So copy and paste hello [Normalize Data][normalize-data] module toocreate a second copy and connect it toohello right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="c4db9-178">Connectez ensuite de sortie de gauche de hello Hello [Normalize Data] [ normalize-data] toohello module droite port d’entrée de hello deuxième [Score Model] [ score-model] module.</span><span class="sxs-lookup"><span data-stu-id="c4db9-178">Connect hello left output of hello second [Normalize Data][normalize-data] module toohello right input port of hello second [Score Model][score-model] module.</span></span>

    ![Deux modules Noter le modèle connectés][7]

### <a name="add-hello-evaluate-model-module"></a><span data-ttu-id="c4db9-180">Ajouter hello évaluer le modèle module</span><span class="sxs-lookup"><span data-stu-id="c4db9-180">Add hello Evaluate Model module</span></span>

<span data-ttu-id="c4db9-181">tooevaluate hello deux résultats de calcul de score et de les comparer, nous utilisons un [modèle Evaluate] [ evaluate-model] module.</span><span class="sxs-lookup"><span data-stu-id="c4db9-181">tooevaluate hello two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="c4db9-182">Recherche hello [modèle Evaluate] [ evaluate-model] module et faites-le glisser sur le canevas de hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-182">Find hello [Evaluate Model][evaluate-model] module and drag it onto hello canvas.</span></span>

2. <span data-ttu-id="c4db9-183">Connectez le port de sortie de hello de hello [Score Model] [ score-model] module associé hello augmentés décision arborescence modèle toohello gauche d’entrée de port de hello [modèle Evaluate] [ evaluate-model] module.</span><span class="sxs-lookup"><span data-stu-id="c4db9-183">Connect hello output port of hello [Score Model][score-model] module associated with hello boosted decision tree model toohello left input port of hello [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="c4db9-184">Se connecter hello autres [Score Model] [ score-model] toohello module droit d’entrée de port.</span><span class="sxs-lookup"><span data-stu-id="c4db9-184">Connect hello other [Score Model][score-model] module toohello right input port.</span></span>  

    ![Module Évaluer le modèle connecté][8]

### <a name="run-hello-experiment-and-check-hello-results"></a><span data-ttu-id="c4db9-186">Exécutez hello expérience et vérifier les résultats de hello</span><span class="sxs-lookup"><span data-stu-id="c4db9-186">Run hello experiment and check hello results</span></span>

<span data-ttu-id="c4db9-187">toorun hello expérience, cliquez sur hello **exécuter** situé sous la zone de dessin hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-187">toorun hello experiment, click hello **RUN** button below hello canvas.</span></span> <span data-ttu-id="c4db9-188">Cette opération peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c4db9-188">It may take a few minutes.</span></span> <span data-ttu-id="c4db9-189">Un indicateur de rotation sur chaque module indique qu’il est en cours d’exécution et ensuite une coche verte indique quand le module de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="c4db9-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when hello module is finished.</span></span> <span data-ttu-id="c4db9-190">Lorsque tous les modules hello possèdent une coche, expérience de hello a terminé son exécution.</span><span class="sxs-lookup"><span data-stu-id="c4db9-190">When all hello modules have a check mark, hello experiment has finished running.</span></span>

<span data-ttu-id="c4db9-191">expérience de Hello doit maintenant ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="c4db9-191">hello experiment should now look something like this:</span></span>  

![Evaluating both models][3]

<span data-ttu-id="c4db9-193">résultats de hello toocheck, cliquez sur le port de sortie hello Hello [modèle Evaluate] [ evaluate-model] module et sélectionnez **visualiser**.</span><span class="sxs-lookup"><span data-stu-id="c4db9-193">toocheck hello results, click hello output port of hello [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="c4db9-194">Hello [modèle Evaluate] [ evaluate-model] module génère une paire de courbes et les mesures qui permettent de résultats de hello toocompare de deux modèles de score hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-194">hello [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you toocompare hello results of hello two scored models.</span></span> <span data-ttu-id="c4db9-195">Vous pouvez afficher les résultats de hello en tant que courbes récepteur opérateur caractéristique (ROC), des courbes de précision et de rappel ou des courbes de courbes d’élévation.</span><span class="sxs-lookup"><span data-stu-id="c4db9-195">You can view hello results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="c4db9-196">Données supplémentaires affichées incluent une matrice de confusion, les valeurs cumulées de zone hello sous la courbe de hello (AUC) et d’autres mesures.</span><span class="sxs-lookup"><span data-stu-id="c4db9-196">Additional data displayed includes a confusion matrix, cumulative values for hello area under hello curve (AUC), and other metrics.</span></span> <span data-ttu-id="c4db9-197">Vous pouvez modifier la valeur de seuil hello par déplacement de curseur hello gauche ou droite et voir comment il affecte ensemble hello de mesures.</span><span class="sxs-lookup"><span data-stu-id="c4db9-197">You can change hello threshold value by moving hello slider left or right and see how it affects hello set of metrics.</span></span>  

<span data-ttu-id="c4db9-198">toohello à droite du graphique de hello, cliquez sur **transformée dataset** ou **transformée dataset toocompare** toohighlight Bonjour associé courbe et toodisplay Bonjour associés métriques ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c4db9-198">toohello right of hello graph, click **Scored dataset** or **Scored dataset toocompare** toohighlight hello associated curve and toodisplay hello associated metrics below.</span></span> <span data-ttu-id="c4db9-199">Dans légende hello pour les courbes de hello, « Transformée dataset » correspond toohello gauche d’un port d’entrée de hello [modèle Evaluate] [ evaluate-model] module - dans le cas présent, il s’agit modèle d’arbre de décision augmenté de hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-199">In hello legend for hello curves, "Scored dataset" corresponds toohello left input port of hello [Evaluate Model][evaluate-model] module - in our case, this is hello boosted decision tree model.</span></span> <span data-ttu-id="c4db9-200">« Transformée dataset toocompare » correspond port d’entrée droite toohello - modèle SVM hello dans notre cas.</span><span class="sxs-lookup"><span data-stu-id="c4db9-200">"Scored dataset toocompare" corresponds toohello right input port - hello SVM model in our case.</span></span> <span data-ttu-id="c4db9-201">Lorsque vous cliquez sur une de ces étiquettes, courbe hello pour ce modèle est mis en surbrillance et les métriques correspondant hello sont affichent, comme indiqué dans le graphique suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-201">When you click one of these labels, hello curve for that model is highlighted and hello corresponding metrics are displayed, as shown in hello following graphic.</span></span>  

![ROC curves for models][4]

<span data-ttu-id="c4db9-203">En examinant ces valeurs, vous pouvez décider quel modèle est le plus proche toogiving que Hello de résultats que vous recherchez.</span><span class="sxs-lookup"><span data-stu-id="c4db9-203">By examining these values, you can decide which model is closest toogiving you hello results you're looking for.</span></span> <span data-ttu-id="c4db9-204">Vous pouvez revenir en arrière et itérez au sein de votre expérience en modifiant les valeurs de paramètre dans des modèles différents hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-204">You can go back and iterate on your experiment by changing parameter values in hello different models.</span></span> 

<span data-ttu-id="c4db9-205">science de Hello et art d’interpréter ces résultats et de paramétrage des performances du modèle hello est étendue de hello en dehors de cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="c4db9-205">hello science and art of interpreting these results and tuning hello model performance is outside hello scope of this walkthrough.</span></span> <span data-ttu-id="c4db9-206">Pour obtenir une aide supplémentaire, vous pouvez lire hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="c4db9-206">For additional help, you might read hello following articles:</span></span>
- [<span data-ttu-id="c4db9-207">Comment tooevaluate modèle de performances dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c4db9-207">How tooevaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="c4db9-208">Choisissez des paramètres toooptimize vos algorithmes dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c4db9-208">Choose parameters toooptimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="c4db9-209">Interprétation des résultats de modèle dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c4db9-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="c4db9-210">Chaque fois que vous exécutez expérience de hello un enregistrement de cette itération est conservée dans hello historique d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c4db9-210">Each time you run hello experiment a record of that iteration is kept in hello Run History.</span></span> <span data-ttu-id="c4db9-211">Vous pouvez afficher ces itérations et revenir tooany d'entre elles, en cliquant sur **afficher l’historique d’exécution** sous la zone de dessin hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-211">You can view these iterations, and return tooany of them, by clicking **VIEW RUN HISTORY** below hello canvas.</span></span> <span data-ttu-id="c4db9-212">Vous pouvez également cliquer sur **exécuter préalable** Bonjour **propriétés** itération de toohello tooreturn volet précédant hello un est ouvert.</span><span class="sxs-lookup"><span data-stu-id="c4db9-212">You can also click **Prior Run** in hello **Properties** pane tooreturn toohello iteration immediately preceding hello one you have open.</span></span>
> 
> <span data-ttu-id="c4db9-213">Vous pouvez effectuer une copie d’une itération de votre expérience en cliquant sur **SAVE AS** sous la zone de dessin hello.</span><span class="sxs-lookup"><span data-stu-id="c4db9-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below hello canvas.</span></span> 
> <span data-ttu-id="c4db9-214">Utiliser d’expérience hello **Résumé** et **Description** propriétés tookeep un enregistrement de ce que vous avez essayé de dans les itérations de votre expérience.</span><span class="sxs-lookup"><span data-stu-id="c4db9-214">Use hello experiment's **Summary** and **Description** properties tookeep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="c4db9-215">Pour en savoir plus, consultez la section [Gérer les itérations des expériences dans Microsoft Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="c4db9-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="c4db9-216">**Ensuite : [déployer hello web service](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="c4db9-216">**Next: [Deploy hello web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

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
