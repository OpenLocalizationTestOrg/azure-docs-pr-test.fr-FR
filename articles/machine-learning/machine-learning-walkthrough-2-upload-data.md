---
title: "Étape 2 : télécharger des données dans une expérience Machine Learning | Microsoft Docs"
description: "Étape 2 de hello développer la procédure pas à pas une solution prédictive : téléchargement stockées les données publiques dans Azure Machine Learning Studio."
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
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="79112-103">Étape de didacticiel pas à pas 2 : téléchargement de données existantes dans une expérience Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="79112-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="79112-104">Il s’agit hello deuxième étape de hello procédure pas à pas, [développer une solution prédictive analytique dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="79112-104">This is hello second step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="79112-105">Créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="79112-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="79112-106">**Télécharger des données existantes**</span><span class="sxs-lookup"><span data-stu-id="79112-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="79112-107">Créer une expérience</span><span class="sxs-lookup"><span data-stu-id="79112-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="79112-108">L’apprentissage et évaluer des modèles de hello</span><span class="sxs-lookup"><span data-stu-id="79112-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="79112-109">Déployer le service Web de hello</span><span class="sxs-lookup"><span data-stu-id="79112-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="79112-110">Accéder au service Web de hello</span><span class="sxs-lookup"><span data-stu-id="79112-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="79112-111">toodevelop un modèle de prévision pour risque de crédit, nous avons besoin de données que nous pouvons utiliser tootrain et ensuite tester le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="79112-111">toodevelop a predictive model for credit risk, we need data that we can use tootrain and then test hello model.</span></span> <span data-ttu-id="79112-112">Cette procédure pas à pas, nous allons utiliser hello « Jeu de données UCI Statlog (données de crédit allemande) » à partir du référentiel d’apprentissage de communications unifiées Irvine hello.</span><span class="sxs-lookup"><span data-stu-id="79112-112">For this walkthrough, we'll use hello "UCI Statlog (German Credit Data) Data Set" from hello UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="79112-113">Vous pouvez le trouver ici : </span><span class="sxs-lookup"><span data-stu-id="79112-113">You can find it here:</span></span>  
<span data-ttu-id="79112-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span><span class="sxs-lookup"><span data-stu-id="79112-114"><a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a></span></span>

<span data-ttu-id="79112-115">Nous allons utiliser le fichier hello nommé **german.data**.</span><span class="sxs-lookup"><span data-stu-id="79112-115">We'll use hello file named **german.data**.</span></span> <span data-ttu-id="79112-116">Télécharger ce fichier tooyour le disque dur local.</span><span class="sxs-lookup"><span data-stu-id="79112-116">Download this file tooyour local hard drive.</span></span>  

<span data-ttu-id="79112-117">Hello **german.data** dataset contient des lignes de 20 variables pour 1000 candidats passées de crédit.</span><span class="sxs-lookup"><span data-stu-id="79112-117">hello **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="79112-118">Ces 20 variables représentent l’ensemble du jeu de données hello de fonctionnalités (hello *vecteur de fonctionnalité*), qui fournit des caractéristiques d’identification pour chaque candidat de crédit.</span><span class="sxs-lookup"><span data-stu-id="79112-118">These 20 variables represent hello dataset's set of features (hello *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="79112-119">Une colonne supplémentaire dans chaque ligne représente un risque de crédit calculée du demandeur hello, avec les 700 candidats identifiés comme un risque de crédit basse et 300 comme un risque élevé.</span><span class="sxs-lookup"><span data-stu-id="79112-119">An additional column in each row represents hello applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="79112-120">site Web de Hello UCI fournit une description des attributs hello du vecteur de fonctionnalité hello pour ces données.</span><span class="sxs-lookup"><span data-stu-id="79112-120">hello UCI website provides a description of hello attributes of hello feature vector for this data.</span></span> <span data-ttu-id="79112-121">Cela inclut des informations financières, l’historique de crédit, le statut professionnel et des informations personnelles.</span><span class="sxs-lookup"><span data-stu-id="79112-121">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="79112-122">Une évaluation binaire a été appliquée à chaque candidat, afin d'indiquer s'il constitue un risque de crédit faible ou élevé.</span><span class="sxs-lookup"><span data-stu-id="79112-122">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="79112-123">Nous utiliserons cette tootrain données un modèle prédictif analytique.</span><span class="sxs-lookup"><span data-stu-id="79112-123">We'll use this data tootrain a predictive analytics model.</span></span> <span data-ttu-id="79112-124">Lorsque nous avons terminé, notre modèle doit être en mesure de tooaccept un vecteur de fonctionnalité pour une nouvelle personne et prédire si elle est un risque de crédit faible ou trop élevée.</span><span class="sxs-lookup"><span data-stu-id="79112-124">When we're done, our model should be able tooaccept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="79112-125">Voici une évolution intéressante.</span><span class="sxs-lookup"><span data-stu-id="79112-125">Here's an interesting twist.</span></span> <span data-ttu-id="79112-126">Bonjour description du jeu de données hello sur hello UCI site Web mentionne prix si nous misclassify risque de crédit d’une personne.</span><span class="sxs-lookup"><span data-stu-id="79112-126">hello description of hello dataset on hello UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="79112-127">Si le modèle de hello prédit un risque élevé pour une personne qui est réellement un risque faible, le modèle de hello a apporté une erreur de classement.</span><span class="sxs-lookup"><span data-stu-id="79112-127">If hello model predicts a high credit risk for someone who is actually a low credit risk, hello model has made a misclassification.</span></span>
<span data-ttu-id="79112-128">Mais mauvaise classification inverse de hello est cinq fois plus coûteuse établissement toohello : si le modèle de hello prédit un risque de crédit faible pour une personne qui est réellement un risque élevé.</span><span class="sxs-lookup"><span data-stu-id="79112-128">But hello reverse misclassification is five times more costly toohello financial institution: if hello model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="79112-129">Par conséquent, nous souhaitons tootrain notre modèle afin que le coût de hello de ce type de ce dernier de mauvaise classification est cinq fois supérieur à celui de la classer par erreur entrées hello autre façon.</span><span class="sxs-lookup"><span data-stu-id="79112-129">So, we want tootrain our model so that hello cost of this latter type of misclassification is five times higher than misclassifying hello other way.</span></span>
<span data-ttu-id="79112-130">Un moyen simple toodo cela lorsque modèle hello dans notre expérience d’apprentissage est en dupliquant (cinq fois) les entrées qui représentent une personne disposant d’un risque élevé.</span><span class="sxs-lookup"><span data-stu-id="79112-130">One simple way toodo this when training hello model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="79112-131">Ensuite, si le modèle de hello misclassifies quelqu'un comme un risque de crédit faible lorsqu’ils sont en fait un risque élevé, hello fait le modèle cette mauvaise classification même cinq fois, une fois pour chaque doublon.</span><span class="sxs-lookup"><span data-stu-id="79112-131">Then, if hello model misclassifies someone as a low credit risk when they're actually a high risk, hello model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="79112-132">Cela augmentera les coûts hello de cette erreur dans les résultats de formation hello.</span><span class="sxs-lookup"><span data-stu-id="79112-132">This will increase hello cost of this error in hello training results.</span></span>


## <a name="convert-hello-dataset-format"></a><span data-ttu-id="79112-133">Convertir le format de jeu de données hello</span><span class="sxs-lookup"><span data-stu-id="79112-133">Convert hello dataset format</span></span>
<span data-ttu-id="79112-134">Hello de jeu de données d’origine utilise un format de séparées par des vide.</span><span class="sxs-lookup"><span data-stu-id="79112-134">hello original dataset uses a blank-separated format.</span></span> <span data-ttu-id="79112-135">Machine Learning Studio fonctionne mieux avec un fichier de valeurs séparées par des virgules (CSV), donc nous allons convertir le jeu de données de hello en remplaçant les espaces par des virgules.</span><span class="sxs-lookup"><span data-stu-id="79112-135">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert hello dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="79112-136">Il existe de nombreuses façons tooconvert ces données.</span><span class="sxs-lookup"><span data-stu-id="79112-136">There are many ways tooconvert this data.</span></span> <span data-ttu-id="79112-137">Consiste à l’aide de hello commande de Windows PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="79112-137">One way is by using hello following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="79112-138">Une autre méthode consiste à l’aide des commandes de sed hello Unix :</span><span class="sxs-lookup"><span data-stu-id="79112-138">Another way is by using hello Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="79112-139">Dans les deux cas, nous avons créé une version séparée par des virgules des données de hello dans un fichier nommé **german.csv** que nous pouvons utiliser dans notre expérience.</span><span class="sxs-lookup"><span data-stu-id="79112-139">In either case, we have created a comma-separated version of hello data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-hello-dataset-toomachine-learning-studio"></a><span data-ttu-id="79112-140">Télécharger hello dataset tooMachine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="79112-140">Upload hello dataset tooMachine Learning Studio</span></span>
<span data-ttu-id="79112-141">Une fois que les données de salutation a été converti tooCSV format, nous devons tooupload dans Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="79112-141">Once hello data has been converted tooCSV format, we need tooupload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="79112-142">Page d’accueil de Machine Learning Studio ouvert hello ([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="79112-142">Open hello Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="79112-143">Cliquez sur le menu de hello ![Menu][1] dans le coin supérieur gauche de hello de fenêtre hello, cliquez sur **Azure Machine Learning**, sélectionnez **Studio**et vous connecter.</span><span class="sxs-lookup"><span data-stu-id="79112-143">Click hello menu ![Menu][1] in hello upper-left corner of hello window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="79112-144">Cliquez sur **+ nouveau** bas hello de fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="79112-144">Click **+NEW** at hello bottom of hello window.</span></span>

4. <span data-ttu-id="79112-145">Sélectionnez **JEU DE DONNÉES**.</span><span class="sxs-lookup"><span data-stu-id="79112-145">Select **DATASET**.</span></span>

5. <span data-ttu-id="79112-146">Sélectionnez **DEPUIS UN FICHIER LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="79112-146">Select **FROM LOCAL FILE**.</span></span>

    ![Ajouter un jeu de données à partir d’un fichier local][2]

6. <span data-ttu-id="79112-148">Bonjour **télécharger un nouveau dataset** boîte de dialogue, cliquez sur **Parcourir** et recherche hello **german.csv** fichier que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="79112-148">In hello **Upload a new dataset** dialog, click **Browse** and find hello **german.csv** file you created.</span></span>

7. <span data-ttu-id="79112-149">Entrez un nom pour le jeu de données hello.</span><span class="sxs-lookup"><span data-stu-id="79112-149">Enter a name for hello dataset.</span></span> <span data-ttu-id="79112-150">Pour les besoins de cette procédure, donnez-lui le nom suivant : « Données de carte de crédit allemande UCI ».</span><span class="sxs-lookup"><span data-stu-id="79112-150">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="79112-151">Pour le type de données, sélectionnez **Fichier CSV générique sans en-tête (.nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="79112-151">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="79112-152">Ajoutez la description de votre choix.</span><span class="sxs-lookup"><span data-stu-id="79112-152">Add a description if you’d like.</span></span>

10. <span data-ttu-id="79112-153">Cliquez sur hello **OK** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="79112-153">Click hello **OK** check mark.</span></span>  

    ![Télécharger le jeu de données hello][3]

<span data-ttu-id="79112-155">Il télécharge des données de hello dans un module de jeu de données que nous pouvons utiliser dans une expérience.</span><span class="sxs-lookup"><span data-stu-id="79112-155">This uploads hello data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="79112-156">Vous pouvez gérer des jeux de données que vous avez téléchargé tooStudio en cliquant sur hello **DATASETS** onglet toohello à gauche de la fenêtre de Studio hello.</span><span class="sxs-lookup"><span data-stu-id="79112-156">You can manage datasets that you've uploaded tooStudio by clicking hello **DATASETS** tab toohello left of hello Studio window.</span></span>

![Gérer des jeux de données][4]

<span data-ttu-id="79112-158">Pour plus d’informations sur l’importation d’autres types de données dans une expérience, consultez [Importez vos données d’apprentissage dans Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="79112-158">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](machine-learning-data-science-import-data.md).</span></span>

<span data-ttu-id="79112-159">**Étape suivante : [créer une expérience](machine-learning-walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="79112-159">**Next: [Create a new experiment](machine-learning-walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
