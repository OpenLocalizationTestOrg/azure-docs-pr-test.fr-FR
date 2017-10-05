---
title: "Étape 2 : télécharger des données dans une expérience Machine Learning | Microsoft Docs"
description: "Étape 2 du guide pas à pas du développement d'une solution prédictive : téléchargement de données publiques stockées dans Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: c2ab5f5252e1ea1ec51f6c3bd489826c70ff011c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="4fcbf-103">Étape de didacticiel pas à pas 2 : téléchargement de données existantes dans une expérience Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4fcbf-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="4fcbf-104">Voici la deuxième étape de la procédure pas à pas [Développement d'une solution d'analyse prédictive dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="4fcbf-104">This is the second step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="4fcbf-105">Créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4fcbf-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="4fcbf-106">**Télécharger des données existantes**</span><span class="sxs-lookup"><span data-stu-id="4fcbf-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="4fcbf-107">Créer une expérience</span><span class="sxs-lookup"><span data-stu-id="4fcbf-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="4fcbf-108">Former et évaluer les modèles</span><span class="sxs-lookup"><span data-stu-id="4fcbf-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="4fcbf-109">Déployer le service web</span><span class="sxs-lookup"><span data-stu-id="4fcbf-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="4fcbf-110">Accéder au service web</span><span class="sxs-lookup"><span data-stu-id="4fcbf-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="4fcbf-111">Pour développer un modèle prédictif pour un risque de crédit, nous avons besoin de données que nous pouvons utiliser pour former et ensuite tester le modèle.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-111">To develop a predictive model for credit risk, we need data that we can use to train and then test the model.</span></span> <span data-ttu-id="4fcbf-112">Pour cette procédure pas à pas, nous allons utiliser le modèle « UCI Statlog (German Credit Data) Data Set » qui se trouve dans le référentiel de UC Irvine Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-112">For this walkthrough, we'll use the "UCI Statlog (German Credit Data) Data Set" from the UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="4fcbf-113">Vous pouvez le trouver ici : </span><span class="sxs-lookup"><span data-stu-id="4fcbf-113">You can find it here:</span></span>  
<span data-ttu-id="4fcbf-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="4fcbf-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="4fcbf-115">Nous allons utiliser le fichier nommé **german.data**.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-115">We'll use the file named **german.data**.</span></span> <span data-ttu-id="4fcbf-116">Téléchargez ce fichier sur votre disque dur.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-116">Download this file to your local hard drive.</span></span>  

<span data-ttu-id="4fcbf-117">Le jeu de données **german.data** contient des lignes de 20 variables pour 1000 candidats à un crédit.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-117">The **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="4fcbf-118">Ces 20 variables représentent l’ensemble des caractéristiques du jeu de données (le *vecteur de fonctionnalité*), qui fournit des caractéristiques permettant d’identifier chaque candidat à un crédit.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-118">These 20 variables represent the dataset's set of features (the *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="4fcbf-119">Une colonne supplémentaire pour chaque ligne représente le risque de crédit calculé de chaque candidat : 700 candidats constituent un faible risque de crédit et 300 un risque élevé.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-119">An additional column in each row represents the applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="4fcbf-120">Le site Web UCI fournit une description des attributs du vecteur de fonctionnalité pour ces données.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-120">The UCI website provides a description of the attributes of the feature vector for this data.</span></span> <span data-ttu-id="4fcbf-121">Cela inclut des informations financières, l’historique de crédit, le statut professionnel et des informations personnelles.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="4fcbf-122">Une évaluation binaire a été appliquée à chaque candidat, afin d'indiquer s'il constitue un risque de crédit faible ou élevé.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="4fcbf-123">Nous allons utiliser ces données pour former un modèle d'analyse prédictive.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-123">We'll use this data to train a predictive analytics model.</span></span> <span data-ttu-id="4fcbf-124">Lorsque nous aurons terminé, notre modèle pourra accepter un vecteur de fonctionnalité pour un nouvel individu et prévoir si celui-ci constitue un risque de crédit faible ou élevé.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-124">When we're done, our model should be able to accept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="4fcbf-125">Voici une évolution intéressante.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-125">Here's an interesting twist.</span></span> <span data-ttu-id="4fcbf-126">Sur le site web UCI, la description du jeu de données détermine les coûts générés par une erreur de classification des risques associés à un crédit accordé.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-126">The description of the dataset on the UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="4fcbf-127">Si le modèle prévoit un crédit à haut risque pour une personne qui présente un risque réduit, cela signifie que la classification est erronée.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-127">If the model predicts a high credit risk for someone who is actually a low credit risk, the model has made a misclassification.</span></span>
<span data-ttu-id="4fcbf-128">Cependant, le fait de prévoir un risque faible pour une personne présentant un risque élevé est cinq fois plus coûteux pour l’institution financière.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-128">But the reverse misclassification is five times more costly to the financial institution: if the model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="4fcbf-129">Nous voulons donc configurer notre modèle de sorte qu’il considère l’erreur de classification ci-dessus comme étant cinq fois plus coûteuse que l’erreur inverse.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-129">So, we want to train our model so that the cost of this latter type of misclassification is five times higher than misclassifying the other way.</span></span>
<span data-ttu-id="4fcbf-130">Il existe une manière assez simple d’y parvenir lorsque nous configurons le modèle de notre exemple, à savoir multiplier par cinq la valeur des entrées représentant une personne qui présente un risque de crédit élevé.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-130">One simple way to do this when training the model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="4fcbf-131">Ensuite, si le modèle considère une personne présentant un risque élevé comme ne représentant qu’un faible risque, il reproduit cette erreur cinq fois, une fois par doublon.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-131">Then, if the model misclassifies someone as a low credit risk when they're actually a high risk, the model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="4fcbf-132">Cela augmentera le coût de cette erreur dans les résultats de formation.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-132">This will increase the cost of this error in the training results.</span></span>


## <a name="convert-the-dataset-format"></a><span data-ttu-id="4fcbf-133">Conversion du format du jeu de données</span><span class="sxs-lookup"><span data-stu-id="4fcbf-133">Convert the dataset format</span></span>
<span data-ttu-id="4fcbf-134">Le jeu de données d'origine utilise un format séparé par des espaces.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-134">The original dataset uses a blank-separated format.</span></span> <span data-ttu-id="4fcbf-135">Machine Learning Studio fonctionne mieux avec un fichier de valeurs séparées par des virgules (CSV). Nous allons donc convertir le jeu de données en remplaçant les espaces par des virgules.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert the dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="4fcbf-136">Il existe de nombreux moyens de convertir ces données.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-136">There are many ways to convert this data.</span></span> <span data-ttu-id="4fcbf-137">L'une des méthodes consiste à utiliser la commande Windows PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="4fcbf-137">One way is by using the following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="4fcbf-138">Vous pouvez aussi utiliser la commande Unix sed :</span><span class="sxs-lookup"><span data-stu-id="4fcbf-138">Another way is by using the Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="4fcbf-139">Dans les deux cas, nous avons créé une version séparée par des virgules des données dans un fichier nommé **german.csv** que nous utiliserons dans notre expérience.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-139">In either case, we have created a comma-separated version of the data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-the-dataset-to-machine-learning-studio"></a><span data-ttu-id="4fcbf-140">Télécharger le jeu de données vers Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="4fcbf-140">Upload the dataset to Machine Learning Studio</span></span>
<span data-ttu-id="4fcbf-141">Une fois les données converties au format CSV, nous devons les télécharger vers Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-141">Once the data has been converted to CSV format, we need to upload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="4fcbf-142">Ouvrez la page d’accueil de Machine Learning Studio ([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="4fcbf-142">Open the Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="4fcbf-143">Cliquez sur le menu ![Menu][1] dans le coin supérieur gauche de la fenêtre, cliquez sur **Azure Machine Learning**, sélectionnez **Studio**, puis connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-143">Click the menu ![Menu][1] in the upper-left corner of the window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="4fcbf-144">Cliquez sur **+NOUVEAU** en bas de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-144">Click **+NEW** at the bottom of the window.</span></span>

4. <span data-ttu-id="4fcbf-145">Sélectionnez **JEU DE DONNÉES**.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="4fcbf-146">Sélectionnez **DEPUIS UN FICHIER LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-146">Select **FROM LOCAL FILE**.</span></span>

    ![Ajouter un jeu de données à partir d’un fichier local][2]

6. <span data-ttu-id="4fcbf-148">Dans la boîte de dialogue **Charger un nouveau jeu de données**, cliquez sur **Parcourir**, puis recherchez le fichier **german.csv** que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-148">In the **Upload a new dataset** dialog, click **Browse** and find the **german.csv** file you created.</span></span>

7. <span data-ttu-id="4fcbf-149">Entrez le nom du jeu de données.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-149">Enter a name for the dataset.</span></span> <span data-ttu-id="4fcbf-150">Pour les besoins de cette procédure, donnez-lui le nom suivant : « Données de carte de crédit allemande UCI ».</span><span class="sxs-lookup"><span data-stu-id="4fcbf-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="4fcbf-151">Pour le type de données, sélectionnez **Fichier CSV générique sans en-tête (.nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="4fcbf-152">Ajoutez la description de votre choix.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="4fcbf-153">Cliquez sur la coche **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-153">Click the **OK** check mark.</span></span>  

    ![Télécharger le jeu de données][3]

<span data-ttu-id="4fcbf-155">Les données sont téléchargées dans un module de jeu de données utilisable dans une expérience.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-155">This uploads the data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="4fcbf-156">Vous pouvez gérer les jeux de données que vous avez téléchargés dans Studio en cliquant sur l’onglet **JEUX DE DONNÉES** à gauche de la fenêtre de Studio.</span><span class="sxs-lookup"><span data-stu-id="4fcbf-156">You can manage datasets that you've uploaded to Studio by clicking the **DATASETS** tab to the left of the Studio window.</span></span>

![Gérer des jeux de données][4]

<span data-ttu-id="4fcbf-158">Pour plus d’informations sur l’importation d’autres types de données dans une expérience, consultez [Importez vos données d’apprentissage dans Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="4fcbf-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="4fcbf-159">**Étape suivante : [créer une expérience](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="4fcbf-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
