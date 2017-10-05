---
title: "Analyse de données avec Azure Machine Learning | Microsoft Docs"
description: "Utilisez Azure Machine Learning pour générer un modèle Machine Learning prédictif basé sur les données stockées dans Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3197948e32fe5c95b111fe5495a0e5f85966a24b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="212e8-103">Analyse des données avec Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="212e8-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="212e8-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="212e8-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="212e8-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="212e8-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="212e8-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="212e8-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="212e8-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="212e8-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="212e8-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="212e8-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="212e8-109">Ce didacticiel utilise Azure Machine Learning pour générer un modèle Machine Learning prédictif basé sur les données stockées dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="212e8-109">This tutorial uses Azure Machine Learning to build a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="212e8-110">Plus précisément, il crée une campagne marketing ciblée pour Adventure Works, le magasin de vélos, en prévoyant si un client est susceptible d’acheter ou non un vélo.</span><span class="sxs-lookup"><span data-stu-id="212e8-110">Specifically, this builds a targeted marketing campaign for Adventure Works, the bike shop, by predicting if a customer is likely to buy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="212e8-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="212e8-111">Prerequisites</span></span>
<span data-ttu-id="212e8-112">Pour parcourir ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="212e8-112">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="212e8-113">un entrepôt SQL Data Warehouse préchargé avec les exemples de données AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="212e8-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="212e8-114">Pour le configurer, consultez [Créer un Azure SQL Data Warehouse][Create a SQL Data Warehouse] et chargez les données d’exemple.</span><span class="sxs-lookup"><span data-stu-id="212e8-114">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="212e8-115">Si vous disposez déjà d’un entrepôt de données, mais sans disposer d’exemples de données, vous pouvez [charger manuellement des exemples de données][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="212e8-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-the-data"></a><span data-ttu-id="212e8-116">1. Obtenir les données</span><span class="sxs-lookup"><span data-stu-id="212e8-116">1. Get the data</span></span>
<span data-ttu-id="212e8-117">Les données sont indiquées dans la vue dbo.vTargetMail de la base de données AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="212e8-117">The data is in the dbo.vTargetMail view in the AdventureWorksDW database.</span></span> <span data-ttu-id="212e8-118">Pour lire ces données :</span><span class="sxs-lookup"><span data-stu-id="212e8-118">To read this data:</span></span>

1. <span data-ttu-id="212e8-119">Connectez-vous à [Azure Machine Learning Studio][Azure Machine Learning studio], puis cliquez sur Mes expériences.</span><span class="sxs-lookup"><span data-stu-id="212e8-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="212e8-120">Cliquez sur **+NOUVEAU** et sélectionnez **Expérience vide**.</span><span class="sxs-lookup"><span data-stu-id="212e8-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="212e8-121">Entrez le nom de votre expérience : Marketing ciblé.</span><span class="sxs-lookup"><span data-stu-id="212e8-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="212e8-122">Faites glisser le module **Lecteur** du volet des modules dans la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="212e8-122">Drag the **Reader** module from the modules pane into the canvas.</span></span>
5. <span data-ttu-id="212e8-123">Spécifiez les détails de votre base de données SQL Data Warehouse dans le volet Propriétés.</span><span class="sxs-lookup"><span data-stu-id="212e8-123">Specify the details of your SQL Data Warehouse database in the Properties pane.</span></span>
6. <span data-ttu-id="212e8-124">Spécifiez la **requête** de base de données pour lire les données intéressantes.</span><span class="sxs-lookup"><span data-stu-id="212e8-124">Specify the database **query** to read the data of interest.</span></span>

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

<span data-ttu-id="212e8-125">Démarrez l’expérience en cliquant sur l’option **Démarrer** sous la zone de dessin de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="212e8-125">Run the experiment by clicking **Run** under the experiment canvas.</span></span>
<span data-ttu-id="212e8-126">![Exécuter l’expérience][1]</span><span class="sxs-lookup"><span data-stu-id="212e8-126">![Run the experiment][1]</span></span>

<span data-ttu-id="212e8-127">Une fois que l’expérience s’est terminée avec succès, cliquez sur le port de sortie au bas du module Reader et sélectionnez **Visualiser** pour voir les données importées.</span><span class="sxs-lookup"><span data-stu-id="212e8-127">After the experiment finishes running successfully, click the output port at the bottom of the Reader module and select **Visualize** to see the imported data.</span></span>
<span data-ttu-id="212e8-128">![Afficher les données importées][3]</span><span class="sxs-lookup"><span data-stu-id="212e8-128">![View imported data][3]</span></span>

## <a name="2-clean-the-data"></a><span data-ttu-id="212e8-129">2. Nettoyer les données</span><span class="sxs-lookup"><span data-stu-id="212e8-129">2. Clean the data</span></span>
<span data-ttu-id="212e8-130">Pour nettoyer les données, supprimez certaines colonnes qui sont inutiles pour le modèle.</span><span class="sxs-lookup"><span data-stu-id="212e8-130">To clean the data, drop some columns that are not relevant for the model.</span></span> <span data-ttu-id="212e8-131">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="212e8-131">To do this:</span></span>

1. <span data-ttu-id="212e8-132">Faites glisser le module **Colonnes de projet** sur la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="212e8-132">Drag the **Project Columns** module into the canvas.</span></span>
2. <span data-ttu-id="212e8-133">Cliquez sur **Lancer le sélecteur de colonne** dans le volet Propriétés pour spécifier les colonnes que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="212e8-133">Click **Launch column selector** in the Properties pane to specify which columns you wish to drop.</span></span>
   <span data-ttu-id="212e8-134">![Colonnes de projet][4]</span><span class="sxs-lookup"><span data-stu-id="212e8-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="212e8-135">Excluez deux colonnes : CustomerAlternateKey et GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="212e8-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="212e8-136">![Supprimer les colonnes inutiles][5]</span><span class="sxs-lookup"><span data-stu-id="212e8-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-the-model"></a><span data-ttu-id="212e8-137">3. Générer le modèle</span><span class="sxs-lookup"><span data-stu-id="212e8-137">3. Build the model</span></span>
<span data-ttu-id="212e8-138">Nous allons fractionner les données dans la proportion 80 et 20 : 80 % pour l’apprentissage d’un modèle Machine Learning et 20 % pour tester le modèle.</span><span class="sxs-lookup"><span data-stu-id="212e8-138">We will split the data 80-20: 80% to train a machine learning model and 20% to test the model.</span></span> <span data-ttu-id="212e8-139">Nous nous engageons à utiliser des algorithmes « À deux classes » pour ce problème de classification binaire.</span><span class="sxs-lookup"><span data-stu-id="212e8-139">We will make use of the “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="212e8-140">Faites glisser le module **Fractionner** dans la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="212e8-140">Drag the **Split** module into the canvas.</span></span>
2. <span data-ttu-id="212e8-141">Entrez 0,8 comme Fraction de lignes dans le premier jeu de données du volet Propriétés.</span><span class="sxs-lookup"><span data-stu-id="212e8-141">Enter 0.8 for Fraction of rows in the first output dataset in the Properties pane.</span></span>
   <span data-ttu-id="212e8-142">![Fractionner les données en jeu d’apprentissage et de test][6]</span><span class="sxs-lookup"><span data-stu-id="212e8-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="212e8-143">Faites glisser le module **Arbre de décision optimisé à deux classes** dans la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="212e8-143">Drag the **Two-Class Boosted Decision Tree** module into the canvas.</span></span>
4. <span data-ttu-id="212e8-144">Faites glisser le module **Effectuer le traitement de données pour apprentissage du modèle** dans la zone de dessin et spécifiez les entrées.</span><span class="sxs-lookup"><span data-stu-id="212e8-144">Drag the **Train Model** module into the canvas and specify the inputs.</span></span> <span data-ttu-id="212e8-145">Cliquez sur l’option **Lancer le sélecteur de colonne** figurant dans le volet Propriétés.</span><span class="sxs-lookup"><span data-stu-id="212e8-145">Then, click **Launch column selector** in the Properties pane.</span></span>
   * <span data-ttu-id="212e8-146">Première entrée : algorithme ML.</span><span class="sxs-lookup"><span data-stu-id="212e8-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="212e8-147">Deuxième entrée : données sur lesquelles essayer l’algorithme.</span><span class="sxs-lookup"><span data-stu-id="212e8-147">Second input: Data to train the algorithm on.</span></span>
     <span data-ttu-id="212e8-148">![Connecter le module Former le modèle][7]</span><span class="sxs-lookup"><span data-stu-id="212e8-148">![Connect the Train Model module][7]</span></span>
5. <span data-ttu-id="212e8-149">Sélectionnez la colonne **BikeBuyer** comme colonne à prédire.</span><span class="sxs-lookup"><span data-stu-id="212e8-149">Select the **BikeBuyer** column as the column to predict.</span></span>
   <span data-ttu-id="212e8-150">![Sélectionner la colonne à prédire][8]</span><span class="sxs-lookup"><span data-stu-id="212e8-150">![Select Column to predict][8]</span></span>

## <a name="4-score-the-model"></a><span data-ttu-id="212e8-151">4. Notation du modèle</span><span class="sxs-lookup"><span data-stu-id="212e8-151">4. Score the model</span></span>
<span data-ttu-id="212e8-152">Maintenant, nous allons voir comment le modèle s’exécute sur les données de test.</span><span class="sxs-lookup"><span data-stu-id="212e8-152">Now, we will test how the model performs on test data.</span></span> <span data-ttu-id="212e8-153">Nous allons comparer l’algorithme de notre choix avec un autre algorithme et voir celui qui fonctionne le mieux.</span><span class="sxs-lookup"><span data-stu-id="212e8-153">We will compare the algorithm of our choice with a different algorithm to see which performs better.</span></span>

1. <span data-ttu-id="212e8-154">Faites glisser le module **Noter le modèle** dans la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="212e8-154">Drag **Score Model** module into the canvas.</span></span>
    <span data-ttu-id="212e8-155">Première entrée : modèle formé Deuxième entrée : données de test ![Notation du modèle][9]</span><span class="sxs-lookup"><span data-stu-id="212e8-155">First input: Trained model Second input: Test data ![Score the model][9]</span></span>
2. <span data-ttu-id="212e8-156">Faites glisser **Machines de points Bayes à deux classes** dans la zone de dessin de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="212e8-156">Drag the **Two-Class Bayes Point Machine** into the experiment canvas.</span></span> <span data-ttu-id="212e8-157">Nous allons comparer comment cet algorithme fonctionne par rapport à l’arbre de décision optimisé à deux classes.</span><span class="sxs-lookup"><span data-stu-id="212e8-157">We will compare how this algorithm performs in comparison to the Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="212e8-158">Copiez et collez les modules de Former le modèle et le modèle Noter le modèle dans la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="212e8-158">Copy and Paste the modules Train Model and Score Model in the canvas.</span></span>
4. <span data-ttu-id="212e8-159">Faites glisser le module **Évaluer le modèle** module dans la zone de dessin pour comparer les deux algorithmes.</span><span class="sxs-lookup"><span data-stu-id="212e8-159">Drag the **Evaluate Model** module into the canvas to compare the two algorithms.</span></span>
5. <span data-ttu-id="212e8-160">**Exécutez** l’expérience.</span><span class="sxs-lookup"><span data-stu-id="212e8-160">**Run** the experiment.</span></span>
   <span data-ttu-id="212e8-161">![Exécuter l’expérience][10]</span><span class="sxs-lookup"><span data-stu-id="212e8-161">![Run the experiment][10]</span></span>
6. <span data-ttu-id="212e8-162">Cliquez sur le port de sortie situé au bas du module Évaluer le modèle, puis sélectionnez Visualiser.</span><span class="sxs-lookup"><span data-stu-id="212e8-162">Click the output port at the bottom of the Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="212e8-163">![Visualiser les résultats de l’évaluation][11]</span><span class="sxs-lookup"><span data-stu-id="212e8-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="212e8-164">Les mesures fournies sont la courbe ROC (caractéristiques du fonctionnement du récepteur), le diagramme de rappel de précision et la courbe d’élévation.</span><span class="sxs-lookup"><span data-stu-id="212e8-164">The metrics provided are the ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="212e8-165">En examinant ces mesures, nous pouvons voir que le premier modèle fonctionne mieux que le second.</span><span class="sxs-lookup"><span data-stu-id="212e8-165">Looking at these metrics, we can see that the first model performed better than the second one.</span></span> <span data-ttu-id="212e8-166">Pour regarder les prévisions du premier modèle, cliquez sur le port de sortie du modèle de notation, puis cliquez sur Visualiser.</span><span class="sxs-lookup"><span data-stu-id="212e8-166">To look at the what the first model predicted, click on output port of the Score Model and click Visualize.</span></span>
<span data-ttu-id="212e8-167">![Visualiser les résultats de la notation][12]</span><span class="sxs-lookup"><span data-stu-id="212e8-167">![Visualize score results][12]</span></span>

<span data-ttu-id="212e8-168">Vous verrez deux colonnes supplémentaires ajoutées à votre groupe de données de test.</span><span class="sxs-lookup"><span data-stu-id="212e8-168">You will see two more columns added to your test dataset.</span></span>

* <span data-ttu-id="212e8-169">Probabilités évaluées : probabilité qu’un client soit un acheteur potentiel de vélo.</span><span class="sxs-lookup"><span data-stu-id="212e8-169">Scored Probabilities: the likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="212e8-170">Étiquette de marquage : classification effectuée par le modèle – acheteur de vélo (1) ou non (0).</span><span class="sxs-lookup"><span data-stu-id="212e8-170">Scored Labels: the classification done by the model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="212e8-171">Ce seuil de probabilité pour l’étiquetage est défini à 50 % et peut être ajusté.</span><span class="sxs-lookup"><span data-stu-id="212e8-171">This probability threshold for labeling is set to 50% and can be adjusted.</span></span>

<span data-ttu-id="212e8-172">En comparant la colonne BikeBuyer (réelle) avec les étiquettes de marquage (prévision), vous pouvez voir comment le modèle a fonctionné.</span><span class="sxs-lookup"><span data-stu-id="212e8-172">Comparing the column BikeBuyer (actual) with the Scored Labels (prediction), you can see how well the model has performed.</span></span> <span data-ttu-id="212e8-173">Au cours des opérations suivantes, vous pouvez utiliser ce modèle pour élaborer des prévisions pour les nouveaux clients et publier ce modèle en tant que service web ou écrire les résultats dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="212e8-173">As next steps, you can use this model to make predictions for new customers and publish this model as a web service or write results back to SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="212e8-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="212e8-174">Next steps</span></span>
<span data-ttu-id="212e8-175">Pour en savoir plus sur la création de modèles Machine Learning prédictifs, reportez-vous à [Introduction à Machine Learning sur Azure][Introduction to Machine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="212e8-175">To learn more about building predictive machine learning models, refer to [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction to Machine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
