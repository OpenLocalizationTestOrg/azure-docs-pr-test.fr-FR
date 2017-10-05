---
title: "Expérience simple dans Machine Learning Studio | Microsoft Docs"
description: "Ce didacticiel sur l’apprentissage automatique vous guidera tout au long d’une expérience de science des données simple. Nous allons prédire le prix d’une voiture à l’aide d’un algorithme de régression."
keywords: "expérience,régression linéaire,algorithmes d’apprentissage automatique,didacticiel d’apprentissage automatique,techniques de modélisation prédictive,expérience de science de données"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 0539e9d04c61d35de56a29d350c07654c095c576
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="3e8b0-105">Didacticiel sur l’apprentissage automatique : Création de votre première expérience de science des données dans Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="3e8b0-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="3e8b0-106">Si vous n’avez encore jamais utilisé **Azure Machine Learning Studio**, ce didacticiel est pour vous.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="3e8b0-107">Dans ce didacticiel, nous allons découvrir comment utiliser Studio afin de créer une expérience de machine learning.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-107">In this tutorial, we'll walk through how to use Studio for the first time to create a machine learning experiment.</span></span> <span data-ttu-id="3e8b0-108">Cette expérience permettra de tester un modèle analytique qui prédira le prix d’un véhicule automobile en fonction de différentes variables, comme la marque et les caractéristiques techniques.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-108">The experiment will test an analytical model that predicts the price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="3e8b0-109">Ce didacticiel vous montre les principes fondamentaux de glisser-déplacer des modules vers votre expérience, et il vous explique comment les connecter, réaliser votre expérience et étudier les résultats.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-109">This tutorial shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="3e8b0-110">Nous n’allons pas aborder le sujet général du machine learning ni expliquer comment sélectionner et utiliser la centaine de modules de manipulation des données et des algorithmes inclus dans Studio.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-110">We're not going to discuss the general topic of machine learning or how to select and use the 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="3e8b0-111">Si vous ne connaissez pas le machine learning, la série de vidéos [Science des données pour les débutants](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) peut être un bon point de départ.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-111">If you're new to machine learning, the video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place to start.</span></span> <span data-ttu-id="3e8b0-112">Cette série de vidéos constitue une excellente introduction au machine learning, qui utilise le langage et les concepts courants.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-112">This video series is a great introduction to machine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="3e8b0-113">Si vous connaissez le Machine Learning et recherchez des informations plus générales sur Machine Learning Studio et sur les algorithmes de Machine Learning qu’il propose, voici quelques ressources utiles :</span><span class="sxs-lookup"><span data-stu-id="3e8b0-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and the machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="3e8b0-114">Qu'est-ce que Machine Learning Studio ?</span><span class="sxs-lookup"><span data-stu-id="3e8b0-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="3e8b0-115">: il s’agit d’une vue d’ensemble de Studio.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="3e8b0-116">[Principes de base de l’apprentissage automatique avec exemples d’algorithmes](machine-learning-basics-infographic-with-algorithm-examples.md) : cette infographie vous permet de découvrir les différents types d’algorithmes de machine learning inclus dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want to learn more about the different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="3e8b0-117">[Guide Machine Learning](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) : ce guide offre des informations semblables à celles de l’infographie ci-avant, mais dans un format interactif.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as the infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="3e8b0-118">[Aide-mémoire d’algorithme Machine Learning](machine-learning-algorithm-cheat-sheet.md) et [Comment choisir les algorithmes dans Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) : cette affiche téléchargeable et l’article qui l’accompagne traitent des algorithmes Studio en détail.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss the Studio algorithms in depth.</span></span>
- <span data-ttu-id="3e8b0-119">[Machine Learning Studio : aide sur les algorithmes et les modules](https://msdn.microsoft.com/library/azure/dn905974.aspx) : il s’agit du document de référence complet pour tous les modules Studio, y compris les algorithmes de machine learning</span><span class="sxs-lookup"><span data-stu-id="3e8b0-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is the complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="3e8b0-120">En quoi Machine Learning Studio est-il utile ?</span><span class="sxs-lookup"><span data-stu-id="3e8b0-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="3e8b0-121">Machine Learning Studio facilite la configuration d’une expérience à l’aide de modules à glisser-déplacer préprogrammés avec des techniques de modélisation prédictive.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-121">Machine Learning Studio makes it easy to set up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="3e8b0-122">Dans un espace de travail interactif visuel, vous effectuer un glisser-déplacer de ***jeux de données*** et de ***modules*** d’analyse vers un canevas interactif.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="3e8b0-123">Vous les associez afin de former une ***expérience*** que vous pouvez exécuter dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-123">You connect them together to form an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="3e8b0-124">Vous ***créez un modèle***, ***le formez***, puis ***lui attribuez une note et le testez***.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-124">You ***create a model***, ***train the model***, and ***score and test the model***.</span></span>

<span data-ttu-id="3e8b0-125">Vous pouvez affiner la conception de votre modèle en modifiant l’expérience et en l’exécutant jusqu’à ce que vous obteniez les résultats escomptés.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-125">You can iterate on your model design, editing the experiment and running it until it gives you the results you're looking for.</span></span> <span data-ttu-id="3e8b0-126">Lorsque votre modèle est prêt, vous pouvez le publier en tant que ***service web*** afin que d’autres utilisateurs puissent envoyer de nouvelles données et recevoir des prédictions en retour.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="3e8b0-127">Ouverture de Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="3e8b0-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="3e8b0-128">Pour commencer avec Studio, accédez à [https://studio.azureml.net](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="3e8b0-128">To get started with Studio, go to [https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="3e8b0-129">Si vous vous êtes déjà connecté à Machine Learning Studio par le passé, cliquez sur **Sign In** (Se connecter).</span><span class="sxs-lookup"><span data-stu-id="3e8b0-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="3e8b0-130">Sinon, cliquez sur **Sign up here** (S’inscrire) et faites votre choix parmi les options gratuites et payantes.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="3e8b0-131">![Connexion à Machine Learning Studio][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="3e8b0-131">![Sign in to Machine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="3e8b0-132">
***Connexion à Machine Learning Studio***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-132">
***Sign in to Machine Learning Studio***</span></span>

## <a name="five-steps-to-create-an-experiment"></a><span data-ttu-id="3e8b0-133">Cinq étapes pour créer une expérience</span><span class="sxs-lookup"><span data-stu-id="3e8b0-133">Five steps to create an experiment</span></span>

<span data-ttu-id="3e8b0-134">Dans ce didacticiel dédié au machine learning, vous allez suivre cinq étapes de base afin de concevoir une expérience dans Machine Learning Studio et ainsi créer, former et noter votre modèle :</span><span class="sxs-lookup"><span data-stu-id="3e8b0-134">In this machine learning tutorial, you'll follow five basic steps to build an experiment in Machine Learning Studio to create, train, and score your model:</span></span>

- <span data-ttu-id="3e8b0-135">**Création d’un modèle**</span><span class="sxs-lookup"><span data-stu-id="3e8b0-135">**Create a model**</span></span>
    - <span data-ttu-id="3e8b0-136">[Étape 1 : obtention des données]</span><span class="sxs-lookup"><span data-stu-id="3e8b0-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="3e8b0-137">[Étape 2 : préparation des données]</span><span class="sxs-lookup"><span data-stu-id="3e8b0-137">[Step 2: Prepare the data]</span></span>
    - <span data-ttu-id="3e8b0-138">[Étape 3 : définition des fonctionnalités]</span><span class="sxs-lookup"><span data-stu-id="3e8b0-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="3e8b0-139">**Formation du modèle**</span><span class="sxs-lookup"><span data-stu-id="3e8b0-139">**Train the model**</span></span>
    - <span data-ttu-id="3e8b0-140">[Étape 4 : sélection et application d’un algorithme d’apprentissage]</span><span class="sxs-lookup"><span data-stu-id="3e8b0-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="3e8b0-141">**Notation et test du modèle**</span><span class="sxs-lookup"><span data-stu-id="3e8b0-141">**Score and test the model**</span></span>
    - <span data-ttu-id="3e8b0-142">[Étape 5 : prédiction des nouveaux prix des voitures]</span><span class="sxs-lookup"><span data-stu-id="3e8b0-142">[Step 5: Predict new automobile prices]</span></span>

<span data-ttu-id="3e8b0-143">[Étape 1 : obtention des données]: #step-1-get-data</span><span class="sxs-lookup"><span data-stu-id="3e8b0-143">[Step 1: Get data]: #step-1-get-data</span></span>
<span data-ttu-id="3e8b0-144">[Étape 2 : préparation des données]: #step-2-prepare-the-data</span><span class="sxs-lookup"><span data-stu-id="3e8b0-144">[Step 2: Prepare the data]: #step-2-prepare-the-data</span></span>
<span data-ttu-id="3e8b0-145">[Étape 3 : définition des fonctionnalités]: #step-3-define-features</span><span class="sxs-lookup"><span data-stu-id="3e8b0-145">[Step 3: Define features]: #step-3-define-features</span></span>
<span data-ttu-id="3e8b0-146">[Étape 4 : sélection et application d’un algorithme d’apprentissage]: #step-4-choose-and-apply-a-learning-algorithm</span><span class="sxs-lookup"><span data-stu-id="3e8b0-146">[Step 4: Choose and apply a learning algorithm]: #step-4-choose-and-apply-a-learning-algorithm</span></span>
<span data-ttu-id="3e8b0-147">[Étape 5 : prédiction des nouveaux prix des voitures]: #step-5-predict-new-automobile-prices</span><span class="sxs-lookup"><span data-stu-id="3e8b0-147">[Step 5: Predict new automobile prices]: #step-5-predict-new-automobile-prices</span></span>

> [!TIP] 
> <span data-ttu-id="3e8b0-148">Vous pouvez obtenir une copie de travail de l’expérience suivante dans la [galerie Cortana Intelligence](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="3e8b0-148">You can find a working copy of the following experiment in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="3e8b0-149">Accédez à **[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** (Votre première expérience de science des données : prédiction sur les prix automobiles) et cliquez sur **Ouvrir dans Studio** pour télécharger une copie de l’expérience dans votre espace de travail Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-149">Go to **[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="3e8b0-150">Étape 1 : obtention des données</span><span class="sxs-lookup"><span data-stu-id="3e8b0-150">Step 1: Get data</span></span>

<span data-ttu-id="3e8b0-151">Tout d’abord, vous devez obtenir les données.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-151">The first thing you need to perform machine learning is data.</span></span>
<span data-ttu-id="3e8b0-152">Vous pouvez utiliser plusieurs exemples de jeux de données inclus dans Machine Learning Studio ou importer des données à partir de sources diverses.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="3e8b0-153">Pour les besoins de cet exemple, nous allons utiliser le jeu de données **Données sur le prix des véhicules automobiles (brutes)** inclus dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-153">For this example, we'll use the sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="3e8b0-154">Ce jeu de données comprend des entrées relatives à plusieurs véhicules, notamment des informations sur la marque, le modèle, les caractéristiques techniques et le prix.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="3e8b0-155">Voici comment obtenir ce jeu de données dans le cadre de votre expérience.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-155">Here's how to get the dataset into your experiment.</span></span>

1. <span data-ttu-id="3e8b0-156">Créez une expérience en cliquant sur l’option **+NOUVEAU** située en bas de la fenêtre Machine Learning Studio, sélectionnez **EXPÉRIENCE**, puis **Expérience vide**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-156">Create a new experiment by clicking **+NEW** at the bottom of the Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="3e8b0-157">Un nom par défaut est attribué à l’expérience : il apparaît en haut du canevas.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-157">The experiment is given a default name that you can see at the top of the canvas.</span></span> <span data-ttu-id="3e8b0-158">Sélectionnez le texte et remplacez-le par un nom plus significatif, par exemple **Prédiction sur les prix automobiles**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-158">Select this text and rename it to something meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="3e8b0-159">Le nom n’a pas besoin d’être unique.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-159">The name doesn't need to be unique.</span></span>

    ![Renommer l’expérience][rename-experiment]

2. <span data-ttu-id="3e8b0-161">Sur la gauche de la zone de dessin de l’expérience se trouve une palette de jeux de données et de modules.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-161">To the left of the experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="3e8b0-162">Tapez la valeur **automobile** dans la zone de recherche se trouvant en haut de cette palette, afin de rechercher le jeu de données **Données sur le prix des véhicules automobiles (brutes)**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-162">Type **automobile** in the Search box at the top of this palette to find the dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="3e8b0-163">Faites glisser ce jeu de données vers le canevas de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-163">Drag this dataset to the experiment canvas.</span></span>

    <span data-ttu-id="3e8b0-164">![Recherchez le jeu de données d’automobile et faites-le glisser vers le canevas de l’expérience][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="3e8b0-164">![Find the automobile dataset and drag it onto the experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="3e8b0-165">***Rechercher le jeu de données automobile et faites-le glisser sur le canevas de l’expérience***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-165">***Find the automobile dataset and drag it onto the experiment canvas***</span></span>

<span data-ttu-id="3e8b0-166">Pour voir à quoi ressemblent ces données, cliquez sur le port de sortie situé en bas du jeu de données d’automobile, puis sélectionnez **Visualiser**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-166">To see what this data looks like, click the output port at the bottom of the automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="3e8b0-167">![Cliquez sur le port de sortie et sélectionnez Visualiser][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="3e8b0-167">![Click the output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="3e8b0-168">
***Cliquez sur le port de sortie et sélectionnez Visualiser***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-168">
***Click the output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="3e8b0-169">Les jeux de données et les modules disposent de ports d’entrée et de sortie représentés par de petits cercles : les ports d’entrée se situent en haut, tandis que les ports de sortie se situent en bas.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-169">Datasets and modules have input and output ports represented by small circles - input ports at the top, output ports at the bottom.</span></span>
<span data-ttu-id="3e8b0-170">Pour créer un flux de données dans votre expérience, connectez le port de sortie d’un module au port d’entrée d’un autre module.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-170">To create a flow of data through your experiment, you'll connect an output port of one module to an input port of another.</span></span>
<span data-ttu-id="3e8b0-171">À tout moment, vous pouvez cliquer sur le port de sortie d’un jeu de données ou d’un module afin de voir à quoi les données ressemblent à ce stade dans le flux de données.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-171">At any time, you can click the output port of a dataset or module to see what the data looks like at that point in the data flow.</span></span>

<span data-ttu-id="3e8b0-172">Dans cet exemple de jeu de données, chaque instance de véhicule automobile apparaît sous la forme d’une ligne, et les variables associées à chaque véhicule automobile apparaissent dans des colonnes.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-172">In this sample dataset, each instance of an automobile appears as a row, and the variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="3e8b0-173">Compte tenu des variables associées à un véhicule automobile spécifique, nous allons essayer de prédire le prix dans la colonne de droite (colonne 26, intitulée « price »).</span><span class="sxs-lookup"><span data-stu-id="3e8b0-173">Given the variables for a specific automobile, we're going to try to predict the price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="3e8b0-174">![Affichez les données automobiles dans la fenêtre de visualisation des données][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="3e8b0-174">![View the automobile data in the data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="3e8b0-175">
***Affichez les données automobiles dans la fenêtre de visualisation des données***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-175">
***View the automobile data in the data visualization window***</span></span>

<span data-ttu-id="3e8b0-176">Fermez la fenêtre de visualisation en cliquant sur le symbole «**x**» dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-176">Close the visualization window by clicking the "**x**" in the upper-right corner.</span></span>

## <a name="step-2-prepare-the-data"></a><span data-ttu-id="3e8b0-177">Étape 2 : préparation des données</span><span class="sxs-lookup"><span data-stu-id="3e8b0-177">Step 2: Prepare the data</span></span>

<span data-ttu-id="3e8b0-178">Pour pouvoir être analysé, un jeu de données nécessite généralement un traitement préalable.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="3e8b0-179">Vous avez peut-être remarqué l’absence de certaines valeurs dans les colonnes des différentes lignes.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-179">For example, you might have noticed the missing values present in the columns of various rows.</span></span> <span data-ttu-id="3e8b0-180">Pour que vous puissiez analyser les données correctement, ces valeurs manquantes doivent être nettoyées.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-180">These missing values need to be cleaned so the model can analyze the data correctly.</span></span> <span data-ttu-id="3e8b0-181">Dans le cas qui nous occupe, nous allons supprimer toutes les lignes dans lesquelles des valeurs sont manquantes.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="3e8b0-182">De plus, la colonne **normalized-losses** contient une grande quantité de valeurs manquantes. Nous allons donc l’exclure du modèle.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-182">Also, the **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from the model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="3e8b0-183">Le nettoyage des valeurs manquantes des données d’entrée est un prérequis pour l’utilisation de la plupart des modules.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-183">Cleaning the missing values from input data is a prerequisite for using most of the modules.</span></span>

<span data-ttu-id="3e8b0-184">Nous commençons par ajouter un module qui supprime la colonne **normalized-losses**, puis nous ajoutons un module qui supprime toute ligne dans laquelle des données manquent.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-184">First we add a module that removes the **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="3e8b0-185">Dans la zone de recherche située sur la partie supérieure de la palette de modules, saisissez la chaîne **sélectionner des colonnes** afin de rechercher le module [Sélectionner des colonnes dans le jeu de données][select-columns], puis faites glisser ce module vers le canevas de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-185">Type **select columns** in the Search box at the top of the module palette to find the [Select Columns in Dataset][select-columns] module, then drag it to the experiment canvas.</span></span> <span data-ttu-id="3e8b0-186">Ce module permet de sélectionner les colonnes de données à inclure ou exclure du modèle.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-186">This module allows us to select which columns of data we want to include or exclude in the model.</span></span>

2. <span data-ttu-id="3e8b0-187">Connectez le port de sortie du jeu de données **Données sur le prix des véhicules automobiles (brutes)** au port d’entrée du module [Sélectionner des colonnes dans le jeu de données][select-columns].</span><span class="sxs-lookup"><span data-stu-id="3e8b0-187">Connect the output port of the **Automobile price data (Raw)** dataset to the input port of the [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="3e8b0-188">![Ajoutez le module Sélectionner des colonnes dans le jeu de données dans le canevas de l’expérience et connectez-le][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="3e8b0-188">![Add the "Select Columns in Dataset" module to the experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="3e8b0-189">***Ajouter le module « Sélectionner les colonnes de jeu de données » dans le canevas de l’expérience et le connecter***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-189">***Add the "Select Columns in Dataset" module to the experiment canvas and connect it***</span></span>

3. <span data-ttu-id="3e8b0-190">Cliquez sur le module [Sélectionner des colonnes dans le jeu de données][select-columns], puis cliquez sur **Lancer le sélecteur de colonne** dans le volet **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-190">Click the [Select Columns in Dataset][select-columns] module and click **Launch column selector** in the **Properties** pane.</span></span>

    - <span data-ttu-id="3e8b0-191">Sur la gauche, cliquez sur **With rules**</span><span class="sxs-lookup"><span data-stu-id="3e8b0-191">On the left, click **With rules**</span></span>
    - <span data-ttu-id="3e8b0-192">Sous **Commencer par**, cliquez sur **Toutes les colonnes**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="3e8b0-193">Vous indiquez ainsi au module [Sélectionner des colonnes dans le jeu de données][select-columns] de transmettre toutes les colonnes, sauf celles que nous nous apprêtons à exclure.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-193">This directs [Select Columns in Dataset][select-columns] to pass through all the columns (except those columns we're about to exclude).</span></span>
    - <span data-ttu-id="3e8b0-194">Dans les listes déroulantes, sélectionnez **Exclure** et **Noms des colonnes**, puis cliquez dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-194">From the drop-downs, select **Exclude** and **column names**, and then click inside the text box.</span></span> <span data-ttu-id="3e8b0-195">Une liste de colonnes s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-195">A list of columns is displayed.</span></span> <span data-ttu-id="3e8b0-196">Sélectionnez la colonne **normalized-losses**, qui est alors ajoutée à la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-196">Select **normalized-losses**, and it's added to the text box.</span></span>
    - <span data-ttu-id="3e8b0-197">Cliquez sur le bouton en forme de coche (OK) pour fermer le sélecteur de colonne (en bas à droite).</span><span class="sxs-lookup"><span data-stu-id="3e8b0-197">Click the check mark (OK) button to close the column selector (on the lower-right).</span></span>

    <span data-ttu-id="3e8b0-198">![Lancez le sélecteur de colonne et excluez la colonne « normalized-losses »][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="3e8b0-198">![Launch the column selector and exclude the "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="3e8b0-199">***Lancer le sélecteur de colonne et d’exclure la colonne « pertes normalisées »***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-199">***Launch the column selector and exclude the "normalized-losses" column***</span></span>

    <span data-ttu-id="3e8b0-200">À présent, le volet de propriétés du module **Sélectionner des colonnes dans le jeu de données** indique qu’il transmettra toutes les colonnes du jeu de données, à l’exception de **normalized-losses**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-200">Now the properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from the dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="3e8b0-201">![Le volet Propriétés indique que la colonne « normalized-losses » est exclue][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="3e8b0-201">![The properties pane shows that the "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="3e8b0-202">***Le volet Propriétés affiche que la colonne « pertes normalisées » est exclue.***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-202">***The properties pane shows that the "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="3e8b0-203">Vous pouvez ajouter un commentaire dans un module en double-cliquant sur ce module, puis en saisissant du texte.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-203">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="3e8b0-204">Ceci peut vous aider à voir d'un seul coup d'œil ce que fait chaque module dans votre expérience.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-204">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="3e8b0-205">Dans ce cas, double-cliquez sur le module [Sélectionner des colonnes dans le jeu de données][select-columns] et saisissez le commentaire suivant : « Exclure les pertes normalisées ».</span><span class="sxs-lookup"><span data-stu-id="3e8b0-205">In this case double-click the [Select Columns in Dataset][select-columns] module and type the comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="3e8b0-206">![Double-cliquez sur un module pour ajouter un commentaire][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="3e8b0-206">![Double-click a module to add a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="3e8b0-207">***Double-cliquez sur un module pour ajouter un commentaire***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-207">***Double-click a module to add a comment***</span></span>

3. <span data-ttu-id="3e8b0-208">Faites glisser le module [Nettoyer les données manquantes][clean-missing-data] vers la zone de dessin de l’expérience et connectez-le au module [Sélectionner des colonnes dans le jeu de données][select-columns].</span><span class="sxs-lookup"><span data-stu-id="3e8b0-208">Drag the [Clean Missing Data][clean-missing-data] module to the experiment canvas and connect it to the [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="3e8b0-209">Dans le volet **Propriétés**, sélectionnez **Supprimer toute la ligne** sous **Mode de nettoyage**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-209">In the **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="3e8b0-210">Cela amène le module [Nettoyage des données manquantes][clean-missing-data] à nettoyer les données en supprimant les lignes pour lesquelles des valeurs manquent.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-210">This directs [Clean Missing Data][clean-missing-data] to clean the data by removing rows that have any missing values.</span></span> <span data-ttu-id="3e8b0-211">Double-cliquez sur le module et saisissez le commentaire suivant : « Supprimer les lignes de valeur manquantes ».</span><span class="sxs-lookup"><span data-stu-id="3e8b0-211">Double-click the module and type the comment "Remove missing value rows."</span></span>

    <span data-ttu-id="3e8b0-212">![Définissez le mode de nettoyage du module « Nettoyage des données manquantes » sur « Supprimer toute la ligne »][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="3e8b0-212">![Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="3e8b0-213">***Définir le mode de nettoyage sur « Supprimer la ligne entière » pour le module « Nettoyage des données manquantes »***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-213">***Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="3e8b0-214">Exécutez l’expérience en cliquant sur **EXÉCUTER** au bas de la page.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-214">Run the experiment by clicking **RUN** at the bottom of the page.</span></span>

    <span data-ttu-id="3e8b0-215">Une fois l’expérience terminée, une coche verte s’affiche en regard de chaque module pour indiquer la réussite de leurs opérations.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-215">When the experiment has finished running, all the modules have a green check mark to indicate that they finished successfully.</span></span> <span data-ttu-id="3e8b0-216">Notez que le statut **Exécution terminée** s’affiche dans le coin supérieur droit de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-216">Notice also the **Finished running** status in the upper-right corner.</span></span>

<span data-ttu-id="3e8b0-217">![Une fois l’exécution terminée, l’expérience doit ressembler à ceci :][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="3e8b0-217">![After running it, the experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="3e8b0-218">
***Une fois l’exécution terminée, l’expérience doit ressembler à ceci :***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-218">
***After running it, the experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="3e8b0-219">Pourquoi exécutons-nous l’expérience maintenant ?</span><span class="sxs-lookup"><span data-stu-id="3e8b0-219">Why did we run the experiment now?</span></span> <span data-ttu-id="3e8b0-220">Lors de l’exécution de l’expérience, les définitions de colonne de nos données sont transmises à partir du jeu de données, par le biais des modules [Sélectionner des colonnes dans le jeu de données][select-columns] et [Nettoyage des données manquantes][clean-missing-data].</span><span class="sxs-lookup"><span data-stu-id="3e8b0-220">By running the experiment, the column definitions for our data pass from the dataset, through the [Select Columns in Dataset][select-columns] module, and through the [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="3e8b0-221">Autrement dit, tous les modules que nous connectons à [Nettoyage des données manquantes][clean-missing-data] disposent de ces mêmes informations.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-221">This means that any modules we connect to [Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="3e8b0-222">Pour l’instant, nous n’avons exécuté que l’action de nettoyage dans l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-222">All we have done in the experiment up to this point is clean the data.</span></span> <span data-ttu-id="3e8b0-223">Si vous souhaitez afficher le jeu de données nettoyé, cliquez sur le port de sortie gauche du module [Nettoyage des données manquantes][clean-missing-data] et sélectionnez **Visualiser**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-223">If you want to view the cleaned dataset, click the left output port of the [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="3e8b0-224">Vous pouvez constater que la colonne **normalized-losses** n’est plus là et qu’il ne manque plus de données.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-224">Notice that the **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="3e8b0-225">Maintenant que les données sont nettoyées, nous pouvons indiquer les fonctionnalités que nous allons utiliser dans le modèle de prévision.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-225">Now that the data is clean, we're ready to specify what features we're going to use in the predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="3e8b0-226">Étape 3 : définition des fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="3e8b0-226">Step 3: Define features</span></span>

<span data-ttu-id="3e8b0-227">Dans Machine Learning, les *fonctionnalités* sont des propriétés individuelles mesurables d’un élément qui vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="3e8b0-228">Dans notre jeu de données, chaque ligne représente un véhicule et chaque colonne une fonctionnalité de ce véhicule.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="3e8b0-229">La recherche du jeu de fonctionnalités adéquat pour la création d’un modèle de prévision requiert certaines expériences et des connaissances sur le problème qui se pose.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about the problem you want to solve.</span></span> <span data-ttu-id="3e8b0-230">Certaines fonctionnalités sont mieux adaptées à la prévision que d’autres.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-230">Some features are better for predicting the target than others.</span></span> <span data-ttu-id="3e8b0-231">En outre, certaines fonctionnalités ont une forte corrélation avec d’autres fonctionnalités et peuvent être supprimées.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="3e8b0-232">Par exemple, city-mpg et highway-mpg sont étroitement liées : nous pouvons donc conserver l’une et supprimer l’autre sans trop affecter la prédiction.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove the other without significantly affecting the prediction.</span></span>

<span data-ttu-id="3e8b0-233">Nous allons développer un modèle utilisant un sous-ensemble de ces fonctionnalités pour notre jeu de données.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-233">Let's build a model that uses a subset of the features in our dataset.</span></span> <span data-ttu-id="3e8b0-234">Vous pouvez revenir en arrière et sélectionner d’autres fonctionnalités, relancer l’expérience et voir si vous obtenez de meilleurs résultats.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-234">You can come back later and select different features, run the experiment again, and see if you get better results.</span></span> <span data-ttu-id="3e8b0-235">Mais pour commencer, nous allons essayer les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e8b0-235">But to start, let's try the following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="3e8b0-236">Faites glisser un autre module [Sélectionner des colonnes dans le jeu de données][select-columns] vers le canevas de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-236">Drag another [Select Columns in Dataset][select-columns] module to the experiment canvas.</span></span> <span data-ttu-id="3e8b0-237">Connectez le port de sortie de gauche du module [Nettoyage des données manquantes][clean-missing-data] à l’entrée du module [Sélectionner des colonnes dans le jeu de données][select-columns].</span><span class="sxs-lookup"><span data-stu-id="3e8b0-237">Connect the left output port of the [Clean Missing Data][clean-missing-data] module to the input of the [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="3e8b0-238">![Connectez le module « Sélectionner des colonnes dans le jeu de données » au module « Nettoyage des données manquantes »][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="3e8b0-238">![Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="3e8b0-239">***Connecter le module « Sélectionner les colonnes de jeu de données » dans le module « Nettoyage des données manquantes »***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-239">***Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="3e8b0-240">Double-cliquez sur le module et saisissez le commentaire suivant : « Sélection des fonctionnalités pour la prévision ».</span><span class="sxs-lookup"><span data-stu-id="3e8b0-240">Double-click the module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="3e8b0-241">Cliquez sur l’option **Lancer le sélecteur de colonne** figurant dans le volet **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-241">Click **Launch column selector** in the **Properties** pane.</span></span>

3. <span data-ttu-id="3e8b0-242">Cliquez sur **With rules**(À l’aide de règles).</span><span class="sxs-lookup"><span data-stu-id="3e8b0-242">Click **With rules**.</span></span>

4. <span data-ttu-id="3e8b0-243">Sous **Commencer par**, cliquez sur **Aucune colonne**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="3e8b0-244">Dans la ligne de filtre, sélectionnez **Inclure** et **Noms des colonnes**, puis sélectionnez notre liste de noms de colonnes dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-244">In the filter row, select **Include** and **column names** and select our list of column names in the text box.</span></span> <span data-ttu-id="3e8b0-245">Cela amène le module à ne pas transmettre toutes les colonnes (fonctions), à l’exception de celles que nous spécifions.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-245">This directs the module to not pass through any columns (features) except the ones that we specify.</span></span>

5. <span data-ttu-id="3e8b0-246">Cliquez sur le bouton en forme de coche (OK) pour continuer.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-246">Click the check mark (OK) button.</span></span>

    <span data-ttu-id="3e8b0-247">![Sélectionnez les colonnes (fonctions) à inclure dans la prédiction][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="3e8b0-247">![Select the columns (features) to include in the prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="3e8b0-248">***Sélectionnez les colonnes (fonctions) à inclure dans la prédiction***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-248">***Select the columns (features) to include in the prediction***</span></span>

<span data-ttu-id="3e8b0-249">Cela produit un jeu de données filtré qui contient uniquement les fonctionnalités que nous souhaitons transmettre à l’algorithme d’apprentissage utilisé à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-249">This produces a filtered dataset containing only the features we want to pass to the learning algorithm we'll use in the next step.</span></span> <span data-ttu-id="3e8b0-250">Plus tard, vous pouvez reprendre la procédure en utilisant une autre sélection de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="3e8b0-251">Étape 4 : sélection et application d’un algorithme d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="3e8b0-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="3e8b0-252">À présent que les données sont prêtes, la construction d'un modèle de prévision passe par la formation et le test.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-252">Now that the data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="3e8b0-253">Nous allons utiliser nos données pour former le modèle, puis tester le modèle pour voir dans quelle mesure il peut prédire les prix.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-253">We'll use our data to train the model, and then we'll test the model to see how closely it's able to predict prices.</span></span>
<!-- For now, don't worry about *why* we need to train and then test a model.-->

<span data-ttu-id="3e8b0-254">La *classification* et la *régression* sont deux types d’algorithmes de machine learning supervisé.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="3e8b0-255">La classification permet de prédire une réponse à partir d'un jeu de catégories défini, comme une couleur (rouge, bleu ou vert).</span><span class="sxs-lookup"><span data-stu-id="3e8b0-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="3e8b0-256">La régression est utilisée pour prédire un nombre.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-256">Regression is used to predict a number.</span></span>

<span data-ttu-id="3e8b0-257">Étant donné que nous voulons prédire un prix, correspondant à un nombre, nous allons utiliser un algorithme de régression.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-257">Because we want to predict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="3e8b0-258">Dans cet exemple, nous allons utiliser un modèle simple de *régression linéaire*.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="3e8b0-259">Pour en savoir plus sur les différents types d’algorithmes de machine learning et pour savoir quand les utiliser, vous pouvez visionner la première vidéo de la série Science des données pour les débutants, intitulée [The five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) (Cinq questions auxquelles la science des données répond).</span><span class="sxs-lookup"><span data-stu-id="3e8b0-259">If you want to learn more about different types of machine learning algorithms and when to use them, you might view the first video in the Data Science for Beginners series, [The five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="3e8b0-260">Vous pouvez également consulter l’infographie [Principes de base du machine learning avec exemples d’algorithmes](machine-learning-basics-infographic-with-algorithm-examples.md), ou consulter l’[aide-mémoire d’algorithme Machine Learning](machine-learning-algorithm-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="3e8b0-260">You might also look at the infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out the [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="3e8b0-261">Nous formons le modèle en lui fournissant un jeu de données qui inclut le prix.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-261">We train the model by giving it a set of data that includes the price.</span></span> <span data-ttu-id="3e8b0-262">Le modèle analyse les données et recherche les corrélations entre les fonctionnalités d’un véhicule automobile et son prix.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-262">The model scans the data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="3e8b0-263">Puis nous testons le modèle : nous lui affectons un ensemble de fonctionnalités pour véhicules automobiles que nous connaissons et nous étudions la précision du modèle concernant la prédiction des prix.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-263">Then we'll test the model - we'll give it a set of features for automobiles we're familiar with and see how close the model comes to predicting the known price.</span></span>

<span data-ttu-id="3e8b0-264">Nous allons utiliser nos données pour la formation et le test en les divisant en jeux de données distincts de formation et de test.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-264">We'll use our data for both training the model and testing it by splitting the data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="3e8b0-265">Sélectionnez et faites glisser le module [Fractionner les données][split] sur le canevas d’expérience et connectez-le au dernier module [Sélectionner des colonnes dans le jeu de données][select-columns].</span><span class="sxs-lookup"><span data-stu-id="3e8b0-265">Select and drag the [Split Data][split] module to the experiment canvas and connect it to the last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="3e8b0-266">Cliquez sur le module [Fractionner les données][split] pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-266">Click the [Split Data][split] module to select it.</span></span> <span data-ttu-id="3e8b0-267">Rechercher **Fraction de lignes dans le premier jeu de données de sortie** (dans le volet **Propriétés** à droite du canevas) et attribuez-lui la valeur 0,75.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-267">Find the **Fraction of rows in the first output dataset** (in the **Properties** pane to the right of the canvas) and set it to 0.75.</span></span> <span data-ttu-id="3e8b0-268">Ainsi, nous allons utiliser 75 % des données pour former le modèle, et 25 % pour le tester. Par la suite, vous pourrez expérimenter d’autres pourcentages.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-268">This way, we'll use 75 percent of the data to train the model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="3e8b0-269">![Attribuez à la part de fractionnement du module « Fractionner les données » la valeur 0,75][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="3e8b0-269">![Set the split fraction of the "Split Data" module to 0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="3e8b0-270">***La fraction de division du module « Données » la valeur 0,75***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-270">***Set the split fraction of the "Split Data" module to 0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="3e8b0-271">En modifiant le paramètre **Valeur de départ aléatoire** , vous pouvez produire différents échantillons aléatoires pour la formation et le test.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-271">By changing the **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="3e8b0-272">Ce paramètre contrôle la valeur de départ du générateur de nombres pseudo-aléatoire.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-272">This parameter controls the seeding of the pseudo-random number generator.</span></span>

2. <span data-ttu-id="3e8b0-273">Exécutez l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-273">Run the experiment.</span></span> <span data-ttu-id="3e8b0-274">Lors de l’expérience, les modules [Sélectionner des colonnes dans le jeu de données][select-columns] et [Fractionner les données][split] transmettent des définitions de colonne aux modules que nous allons ajouter par la suite.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-274">When the experiment is run, the [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions to the modules we'll be adding next.</span></span>  

3. <span data-ttu-id="3e8b0-275">Pour sélectionner l’algorithme d’apprentissage, développez la catégorie **Machine Learning** dans la palette des modules, à gauche de la zone de dessin, puis développez **Initialiser le modèle**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-275">To select the learning algorithm, expand the **Machine Learning** category in the module palette to the left of the canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="3e8b0-276">Différentes catégories de modules s'affichent, permettant d'initialiser des algorithmes d'apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-276">This displays several categories of modules that can be used to initialize machine learning algorithms.</span></span> <span data-ttu-id="3e8b0-277">Pour les besoins de cet exemple, sélectionnez le module [Régression linéaire][linear-regression] sous la catégorie **Régression**, puis faites-le glisser vers le canevas de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-277">For this experiment, select the [Linear Regression][linear-regression] module under the **Regression** category, and drag it to the experiment canvas.</span></span>
<span data-ttu-id="3e8b0-278">Vous pouvez également rechercher le module en tapant « régression linéaire » dans la zone de recherche de la palette.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-278">(You can also find the module by typing "linear regression" in the palette Search box.)</span></span>

4. <span data-ttu-id="3e8b0-279">Recherchez et faites glisser le module [Effectuer le traitement de données pour apprentissage du modèle][train-model] jusqu’à la zone de dessin de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-279">Find and drag the [Train Model][train-model] module to the experiment canvas.</span></span> <span data-ttu-id="3e8b0-280">Connectez la sortie du module [Régression linéaire][linear-regression] à l’entrée de gauche du module [Former le modèle][train-model], puis connectez la sortie des données de formation (port gauche) du module [Fractionner les données][split] à l’entrée de droite du module [Former le modèle][train-model].</span><span class="sxs-lookup"><span data-stu-id="3e8b0-280">Connect the output of the [Linear Regression][linear-regression] module to the left input of the [Train Model][train-model] module, and connect the training data output (left port) of the [Split Data][split] module to the right input of the [Train Model][train-model] module.</span></span>

    <span data-ttu-id="3e8b0-281">![Connectez le module « Former le modèle » aux modules « Régression linéaire » et « Fractionner les données »][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="3e8b0-281">![Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="3e8b0-282">***Connectez le module de « Train Model » aux modules de « Régression linéaire » et de « Données »***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-282">***Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="3e8b0-283">Cliquez sur le module [Effectuer le traitement de données][train-model] pour apprentissage du modèle, cliquez sur l’option **Lancer le sélecteur de colonne** du volet **Propriétés** et sélectionnez la colonne **Price**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-283">Click the [Train Model][train-model] module, click **Launch column selector** in the **Properties** pane, and then select the **price** column.</span></span> <span data-ttu-id="3e8b0-284">Il s’agit de la valeur que notre modèle va prévoir.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-284">This is the value that our model is going to predict.</span></span>

    <span data-ttu-id="3e8b0-285">Vous pouvez sélectionner la colonne **price** dans le sélecteur de colonne en la faisant passer de la liste **Colonnes disponibles** à la liste **Colonnes sélectionnées**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-285">You select the **price** column in the column selector by moving it from the **Available columns** list to the **Selected columns** list.</span></span>

    <span data-ttu-id="3e8b0-286">![Sélectionnez la colonne price pour le module « Former le modèle »][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="3e8b0-286">![Select the price column for the "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="3e8b0-287">***Sélectionnez la colonne du prix pour le module « Train Model »***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-287">***Select the price column for the "Train Model" module***</span></span>

6. <span data-ttu-id="3e8b0-288">Exécutez l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-288">Run the experiment.</span></span>

<span data-ttu-id="3e8b0-289">Nous disposons à présent d’un modèle de régression formé qui permet de noter de nouvelles données automobiles pour effectuer des prédictions de prix.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-289">We now have a trained regression model that can be used to score new automobile data to make price predictions.</span></span>

<span data-ttu-id="3e8b0-290">![Une fois l’exécution terminée, l’expérience doit ressembler à ceci :][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="3e8b0-290">![After running, the experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="3e8b0-291">
***Une fois l’exécution terminée, l’expérience doit ressembler à ceci :***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-291">
***After running, the experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="3e8b0-292">Étape 5 : prédiction des nouveaux prix des voitures</span><span class="sxs-lookup"><span data-stu-id="3e8b0-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="3e8b0-293">À présent que nous avons formé le modèle à l'aide de 75 % de nos données, nous pouvons l'utiliser pour la notation du reste de nos données (25 %), afin de voir s'il fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-293">Now that we've trained the model using 75 percent of our data, we can use it to score the other 25 percent of the data to see how well our model functions.</span></span>

1. <span data-ttu-id="3e8b0-294">Recherchez et faites glisser le module [Noter le modèle][score-model] vers le canevas de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-294">Find and drag the [Score Model][score-model] module to the experiment canvas.</span></span> <span data-ttu-id="3e8b0-295">Connectez la sortie du module [Former le modèle][train-model] au port d’entrée de gauche [Noter le modèle][score-model].</span><span class="sxs-lookup"><span data-stu-id="3e8b0-295">Connect the output of the [Train Model][train-model] module to the left input port of [Score Model][score-model].</span></span> <span data-ttu-id="3e8b0-296">Connectez la sortie de données de test (port de droite) du module [Split Data][split] au port d’entrée de droite de [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="3e8b0-296">Connect the test data output (right port) of the [Split Data][split] module to the right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="3e8b0-297">![Connectez le module « Noter le modèle » aux modules « Former le modèle » et « Fractionner les données »][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="3e8b0-297">![Connect the "Score Model" module to both the "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="3e8b0-298">***Connectez le module de « Modèle de Score » aux modules « Train Model » et de « Données »***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-298">***Connect the "Score Model" module to both the "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="3e8b0-299">Pour exécuter l’expérience et afficher la sortie du module [Score Model][score-model] (cliquez sur le port de sortie de [Score Model][score-model] et sélectionnez **Visualiser**).</span><span class="sxs-lookup"><span data-stu-id="3e8b0-299">Run the experiment and view the output from the [Score Model][score-model] module (click the output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="3e8b0-300">La sortie affiche les valeurs de prévision associées au prix, ainsi que les valeurs connues des données de test.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-300">The output shows the predicted values for price and the known values from the test data.</span></span>  

    <span data-ttu-id="3e8b0-301">![Sortie du module « Noter le modèle »][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="3e8b0-301">![Output of the "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="3e8b0-302">***Sortie du module « Modèle de Score »***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-302">***Output of the "Score Model" module***</span></span>

3. <span data-ttu-id="3e8b0-303">Enfin, nous testons la qualité des résultats.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-303">Finally, we test the quality of the results.</span></span> <span data-ttu-id="3e8b0-304">Sélectionnez et faites glisser le module [Évaluer le modèle][evaluate-model] vers le canevas de l’expérience, puis connectez la sortie du module [Noter le modèle][score-model] à l’entrée de gauche du module [Évaluer le modèle][evaluate-model].</span><span class="sxs-lookup"><span data-stu-id="3e8b0-304">Select and drag the [Evaluate Model][evaluate-model] module to the experiment canvas, and connect the output of the [Score Model][score-model] module to the left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="3e8b0-305">Il existe deux ports d’entrée sur le module [Évaluer le modèle][evaluate-model], car ce dernier peut être utilisé pour comparer deux modèles.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-305">There are two input ports on the [Evaluate Model][evaluate-model] module because it can be used to compare two models side by side.</span></span> <span data-ttu-id="3e8b0-306">Plus tard, vous pourrez ajouter un autre algorithme à l’expérience et utiliser [Évaluer le modèle][evaluate-model] pour déterminer quel module donne les meilleurs résultats.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-306">Later, you can add another algorithm to the experiment and use [Evaluate Model][evaluate-model] to see which one gives better results.</span></span>

4. <span data-ttu-id="3e8b0-307">Exécutez l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-307">Run the experiment.</span></span>

<span data-ttu-id="3e8b0-308">Pour afficher la sortie du module [Evaluate Model][evaluate-model], cliquez sur le port de sortie, puis sélectionnez **Visualiser**.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-308">To view the output from the [Evaluate Model][evaluate-model] module, click the output port, and then select **Visualize**.</span></span>

<span data-ttu-id="3e8b0-309">![Résultats de l’évaluation de l’expérience][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="3e8b0-309">![Evaluation results for the experiment][evaluation-results]
</span></span><br/><span data-ttu-id="3e8b0-310">
***Résultats de l’évaluation de l’expérience***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-310">
***Evaluation results for the experiment***</span></span>

<span data-ttu-id="3e8b0-311">Les statistiques suivantes s’affichent pour notre modèle :</span><span class="sxs-lookup"><span data-stu-id="3e8b0-311">The following statistics are shown for our model:</span></span>

- <span data-ttu-id="3e8b0-312">**Erreur d’absolue moyenne** (EAM) : la moyenne des erreurs absolues (une *erreur* correspond à la différence entre la valeur prévue et la valeur réelle).</span><span class="sxs-lookup"><span data-stu-id="3e8b0-312">**Mean Absolute Error** (MAE): The average of absolute errors (an *error* is the difference between the predicted value and the actual value).</span></span>
- <span data-ttu-id="3e8b0-313">**Racine de l’erreur quadratique moyenne** (RMSE) : la racine carrée de la moyenne des erreurs carrées des prévisions effectuées sur le jeu de données de test.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-313">**Root Mean Squared Error** (RMSE): The square root of the average of squared errors of predictions made on the test dataset.</span></span>
- <span data-ttu-id="3e8b0-314">**Erreur absolue relative**: la moyenne des erreurs absolues relative à la différence absolue entre les valeurs réelles et la moyenne de toutes les valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-314">**Relative Absolute Error**: The average of absolute errors relative to the absolute difference between actual values and the average of all actual values.</span></span>
- <span data-ttu-id="3e8b0-315">**Erreur carrée relative**: la moyenne des erreurs carrées relative à la différence carrée entre les valeurs réelles et la moyenne de toutes les valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-315">**Relative Squared Error**: The average of squared errors relative to the squared difference between the actual values and the average of all actual values.</span></span>
- <span data-ttu-id="3e8b0-316">**Coefficient de détermination** : aussi nommé **valeur R au carré**, il s’agit d’une mesure statistique indiquant à quel point un modèle correspond aux données.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-316">**Coefficient of Determination**: Also known as the **R squared value**, this is a statistical metric indicating how well a model fits the data.</span></span>

<span data-ttu-id="3e8b0-317">Pour chacune des statistiques liées aux erreurs, les valeurs les plus petites sont privilégiées.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-317">For each of the error statistics, smaller is better.</span></span> <span data-ttu-id="3e8b0-318">En effet, une valeur plus petite indique un degré de correspondance plus étroit avec la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-318">A smaller value indicates that the predictions more closely match the actual values.</span></span> <span data-ttu-id="3e8b0-319">Plus la valeur du **Coefficient de détermination**, est proche de un (1.0), plus la prévision est correcte.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-319">For **Coefficient of Determination**, the closer its value is to one (1.0), the better the predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="3e8b0-320">Expérience finale</span><span class="sxs-lookup"><span data-stu-id="3e8b0-320">Final experiment</span></span>

<span data-ttu-id="3e8b0-321">L’expérience finale doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="3e8b0-321">The final experiment should look something like this:</span></span>

<span data-ttu-id="3e8b0-322">![Expérience finale][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="3e8b0-322">![The final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="3e8b0-323">
***Expérience finale***</span><span class="sxs-lookup"><span data-stu-id="3e8b0-323">
***The final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e8b0-324">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3e8b0-324">Next steps</span></span>

<span data-ttu-id="3e8b0-325">À présent que vous avez terminé le premier didacticiel sur le machine learning et que vous avez configuré votre expérience, vous pouvez continuer à améliorer le modèle, puis le déployer en tant que service web prédictif.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-325">Now that you've completed the first machine learning tutorial and have your experiment set up, you can continue to improve the model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="3e8b0-326">**Création d’une itération pour améliorer le modèle** : par exemple, vous pouvez modifier les fonctionnalités que vous utilisez dans votre prédiction.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-326">**Iterate to try to improve the model** - For example, you can change the features you use in your prediction.</span></span> <span data-ttu-id="3e8b0-327">Ou vous pouvez modifier les propriétés de l'algorithme [Régression linéaire][linear-regression], ou essayer un autre algorithme.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-327">Or you can modify the properties of the [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="3e8b0-328">Vous pouvez même ajouter plusieurs algorithmes d'apprentissage automatique à la fois à votre expérience et comparer deux d’entre eux à l'aide du module [Evaluate Model][evaluate-model].</span><span class="sxs-lookup"><span data-stu-id="3e8b0-328">You can even add multiple machine learning algorithms to your experiment at one time and compare two of them by using the [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="3e8b0-329">Pour découvrir comment comparer plusieurs modèles dans le cadre d’une expérience unique, consultez [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) (Comparer les régresseurs) dans la [galerie Cortana Intelligence](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="3e8b0-329">For an example of how to compare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="3e8b0-330">Pour copier une itération de votre expérience, utilisez le bouton **ENREGISTRER SOUS** au bas de la page.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-330">To copy any iteration of your experiment, use the **SAVE AS** button at the bottom of the page.</span></span> <span data-ttu-id="3e8b0-331">Vous pouvez afficher toutes les itérations de votre expérience en cliquant sur **AFFICHER L’HISTORIQUE D’EXÉCUTION** au bas de la page.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-331">You can see all the iterations of your experiment by clicking **VIEW RUN HISTORY** at the bottom of the page.</span></span> <span data-ttu-id="3e8b0-332">Pour en savoir plus, consultez la section [Gérer les itérations des expériences dans Microsoft Azure Machine Learning Studio][runhistory].</span><span class="sxs-lookup"><span data-stu-id="3e8b0-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="3e8b0-333">**Déploiement du modèle en tant que service web prédictif** : une fois satisfait de votre modèle, vous pouvez le déployer en tant que service web permettant de prédire l’évolution des prix dans le secteur automobile, au moyen de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-333">**Deploy the model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service to be used to predict automobile prices by using new data.</span></span> <span data-ttu-id="3e8b0-334">Consultez la section [Déployer un service web Microsoft Azure Machine Learning][publish] pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="3e8b0-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="3e8b0-335">Vous souhaitez en savoir plus ?</span><span class="sxs-lookup"><span data-stu-id="3e8b0-335">Want to learn more?</span></span> <span data-ttu-id="3e8b0-336">Pour obtenir un guide complet et détaillé du processus de création, formation, notation et déploiement d’un modèle, consultez [Développer une solution prédictive à l’aide d’Azure Machine Learning][walkthrough].</span><span class="sxs-lookup"><span data-stu-id="3e8b0-336">For a more extensive and detailed walkthrough of the process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs to PNGs to remove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs to PNGs to remove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
