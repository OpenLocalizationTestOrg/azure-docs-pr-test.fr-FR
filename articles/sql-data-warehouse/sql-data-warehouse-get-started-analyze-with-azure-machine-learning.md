---
title: "aaaAnalyze des données avec Azure Machine Learning | Documents Microsoft"
description: "Utilisez toobuild d’Azure Machine Learning un modèle basé sur les données stockées dans Azure SQL Data Warehouse prédictive d’apprentissage."
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
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="11ff6-103">Analyse des données avec Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="11ff6-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11ff6-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="11ff6-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="11ff6-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="11ff6-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="11ff6-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11ff6-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="11ff6-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="11ff6-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="11ff6-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="11ff6-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="11ff6-109">Ce didacticiel utilise Azure Machine Learning de toobuild un modèle basé sur les données stockées dans Azure SQL Data Warehouse prédictive d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="11ff6-109">This tutorial uses Azure Machine Learning toobuild a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="11ff6-110">Plus précisément, cela génère une campagne de marketing ciblée pour Adventure Works, magasin de vélo hello, la prédiction si un client est toobuy probablement un vélo ou non.</span><span class="sxs-lookup"><span data-stu-id="11ff6-110">Specifically, this builds a targeted marketing campaign for Adventure Works, hello bike shop, by predicting if a customer is likely toobuy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="11ff6-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="11ff6-111">Prerequisites</span></span>
<span data-ttu-id="11ff6-112">toostep dans ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="11ff6-112">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="11ff6-113">un entrepôt SQL Data Warehouse préchargé avec les exemples de données AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="11ff6-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="11ff6-114">tooprovision, consultez [créer un entrepôt de données SQL] [ Create a SQL Data Warehouse] et choisissez les données d’exemple hello tooload.</span><span class="sxs-lookup"><span data-stu-id="11ff6-114">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="11ff6-115">Si vous disposez déjà d’un entrepôt de données, mais sans disposer d’exemples de données, vous pouvez [charger manuellement des exemples de données][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="11ff6-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-hello-data"></a><span data-ttu-id="11ff6-116">1. Obtenir des données de hello</span><span class="sxs-lookup"><span data-stu-id="11ff6-116">1. Get hello data</span></span>
<span data-ttu-id="11ff6-117">les données de salutation sont en mode de dbo.vTargetMail hello dans la base de données AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="11ff6-117">hello data is in hello dbo.vTargetMail view in hello AdventureWorksDW database.</span></span> <span data-ttu-id="11ff6-118">tooread ces données :</span><span class="sxs-lookup"><span data-stu-id="11ff6-118">tooread this data:</span></span>

1. <span data-ttu-id="11ff6-119">Connectez-vous à [Azure Machine Learning Studio][Azure Machine Learning studio], puis cliquez sur Mes expériences.</span><span class="sxs-lookup"><span data-stu-id="11ff6-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="11ff6-120">Cliquez sur **+NOUVEAU** et sélectionnez **Expérience vide**.</span><span class="sxs-lookup"><span data-stu-id="11ff6-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="11ff6-121">Entrez le nom de votre expérience : Marketing ciblé.</span><span class="sxs-lookup"><span data-stu-id="11ff6-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="11ff6-122">Hello de glisser **lecteur** module à partir du volet de modules hello dans la zone de dessin hello.</span><span class="sxs-lookup"><span data-stu-id="11ff6-122">Drag hello **Reader** module from hello modules pane into hello canvas.</span></span>
5. <span data-ttu-id="11ff6-123">Spécifiez les détails de hello de votre base de données de l’entrepôt de données SQL dans le volet de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="11ff6-123">Specify hello details of your SQL Data Warehouse database in hello Properties pane.</span></span>
6. <span data-ttu-id="11ff6-124">Spécifiez la base de données hello **requête** tooread les données de salutation dignes d’intérêt.</span><span class="sxs-lookup"><span data-stu-id="11ff6-124">Specify hello database **query** tooread hello data of interest.</span></span>

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

<span data-ttu-id="11ff6-125">Exécutez hello expérience en cliquant sur **exécuter** sous le canevas de l’expérience hello.</span><span class="sxs-lookup"><span data-stu-id="11ff6-125">Run hello experiment by clicking **Run** under hello experiment canvas.</span></span>
<span data-ttu-id="11ff6-126">![Exécutez hello expérience][1]</span><span class="sxs-lookup"><span data-stu-id="11ff6-126">![Run hello experiment][1]</span></span>

<span data-ttu-id="11ff6-127">Une fois que l’expérience de hello est terminée avec succès, cliquez sur le port de sortie hello bas hello de module de lecture hello et sélectionnez **visualiser** toosee hello importé des données.</span><span class="sxs-lookup"><span data-stu-id="11ff6-127">After hello experiment finishes running successfully, click hello output port at hello bottom of hello Reader module and select **Visualize** toosee hello imported data.</span></span>
<span data-ttu-id="11ff6-128">![Afficher les données importées][3]</span><span class="sxs-lookup"><span data-stu-id="11ff6-128">![View imported data][3]</span></span>

## <a name="2-clean-hello-data"></a><span data-ttu-id="11ff6-129">2. Données de salutation nettoyer</span><span class="sxs-lookup"><span data-stu-id="11ff6-129">2. Clean hello data</span></span>
<span data-ttu-id="11ff6-130">les données de salutation tooclean, de supprimer certaines colonnes ne sont pas pertinentes pour le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="11ff6-130">tooclean hello data, drop some columns that are not relevant for hello model.</span></span> <span data-ttu-id="11ff6-131">toodo cela :</span><span class="sxs-lookup"><span data-stu-id="11ff6-131">toodo this:</span></span>

1. <span data-ttu-id="11ff6-132">Hello de glisser **Project Columns** module dans la zone de dessin hello.</span><span class="sxs-lookup"><span data-stu-id="11ff6-132">Drag hello **Project Columns** module into hello canvas.</span></span>
2. <span data-ttu-id="11ff6-133">Cliquez sur **sélecteur de colonne lancement** dans toospecify de volet de propriétés hello les colonnes que vous souhaitez toodrop.</span><span class="sxs-lookup"><span data-stu-id="11ff6-133">Click **Launch column selector** in hello Properties pane toospecify which columns you wish toodrop.</span></span>
   <span data-ttu-id="11ff6-134">![Colonnes de projet][4]</span><span class="sxs-lookup"><span data-stu-id="11ff6-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="11ff6-135">Excluez deux colonnes : CustomerAlternateKey et GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="11ff6-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="11ff6-136">![Supprimer les colonnes inutiles][5]</span><span class="sxs-lookup"><span data-stu-id="11ff6-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-hello-model"></a><span data-ttu-id="11ff6-137">3. Générer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="11ff6-137">3. Build hello model</span></span>
<span data-ttu-id="11ff6-138">Fractionnées hello données 80-20 : 80 % tootrain un modèle d’apprentissage et 20 % tootest hello modèle.</span><span class="sxs-lookup"><span data-stu-id="11ff6-138">We will split hello data 80-20: 80% tootrain a machine learning model and 20% tootest hello model.</span></span> <span data-ttu-id="11ff6-139">Nous mettrons à utiliser des algorithmes de « Two-Class » hello pour ce problème de classification binaire.</span><span class="sxs-lookup"><span data-stu-id="11ff6-139">We will make use of hello “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="11ff6-140">Hello de glisser **fractionnement** module dans la zone de dessin hello.</span><span class="sxs-lookup"><span data-stu-id="11ff6-140">Drag hello **Split** module into hello canvas.</span></span>
2. <span data-ttu-id="11ff6-141">Entrez 0,8 pour la Fraction de lignes dans le premier jeu de données sortie hello dans le volet de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="11ff6-141">Enter 0.8 for Fraction of rows in hello first output dataset in hello Properties pane.</span></span>
   <span data-ttu-id="11ff6-142">![Fractionner les données en jeu d’apprentissage et de test][6]</span><span class="sxs-lookup"><span data-stu-id="11ff6-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="11ff6-143">Hello de glisser **Two-Class Boosted Decision Tree** module dans la zone de dessin hello.</span><span class="sxs-lookup"><span data-stu-id="11ff6-143">Drag hello **Two-Class Boosted Decision Tree** module into hello canvas.</span></span>
4. <span data-ttu-id="11ff6-144">Hello de glisser **Train Model** module dans hello canevas et spécifier les entrées de hello.</span><span class="sxs-lookup"><span data-stu-id="11ff6-144">Drag hello **Train Model** module into hello canvas and specify hello inputs.</span></span> <span data-ttu-id="11ff6-145">Ensuite, cliquez sur **sélecteur de colonne lancement** dans le volet de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="11ff6-145">Then, click **Launch column selector** in hello Properties pane.</span></span>
   * <span data-ttu-id="11ff6-146">Première entrée : algorithme ML.</span><span class="sxs-lookup"><span data-stu-id="11ff6-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="11ff6-147">Deuxième entrée : algorithme hello tootrain des données sur.</span><span class="sxs-lookup"><span data-stu-id="11ff6-147">Second input: Data tootrain hello algorithm on.</span></span>
     <span data-ttu-id="11ff6-148">![Connexion du module Train Model de hello][7]</span><span class="sxs-lookup"><span data-stu-id="11ff6-148">![Connect hello Train Model module][7]</span></span>
5. <span data-ttu-id="11ff6-149">Sélectionnez hello **BikeBuyer** colonne comme hello toopredict de colonne.</span><span class="sxs-lookup"><span data-stu-id="11ff6-149">Select hello **BikeBuyer** column as hello column toopredict.</span></span>
   <span data-ttu-id="11ff6-150">![Sélectionnez la colonne toopredict][8]</span><span class="sxs-lookup"><span data-stu-id="11ff6-150">![Select Column toopredict][8]</span></span>

## <a name="4-score-hello-model"></a><span data-ttu-id="11ff6-151">4. Modèle de score hello</span><span class="sxs-lookup"><span data-stu-id="11ff6-151">4. Score hello model</span></span>
<span data-ttu-id="11ff6-152">Maintenant, nous allez tester le fonctionne d’un modèle de hello sur les données de test.</span><span class="sxs-lookup"><span data-stu-id="11ff6-152">Now, we will test how hello model performs on test data.</span></span> <span data-ttu-id="11ff6-153">Nous allons comparer algorithme hello de notre choix avec un toosee autre algorithme qui offre de meilleures performances.</span><span class="sxs-lookup"><span data-stu-id="11ff6-153">We will compare hello algorithm of our choice with a different algorithm toosee which performs better.</span></span>

1. <span data-ttu-id="11ff6-154">Faites glisser **Score Model** module dans la zone de dessin hello.</span><span class="sxs-lookup"><span data-stu-id="11ff6-154">Drag **Score Model** module into hello canvas.</span></span>
    <span data-ttu-id="11ff6-155">Première entrée : la deuxième entrée du modèle objet d’un apprentissage : données de Test ![modèle hello de Score][9]</span><span class="sxs-lookup"><span data-stu-id="11ff6-155">First input: Trained model Second input: Test data ![Score hello model][9]</span></span>
2. <span data-ttu-id="11ff6-156">Hello de glisser **Two-Class Bayes Point Machine** dans le canevas de l’expérience hello.</span><span class="sxs-lookup"><span data-stu-id="11ff6-156">Drag hello **Two-Class Bayes Point Machine** into hello experiment canvas.</span></span> <span data-ttu-id="11ff6-157">Nous allons comparer le fonctionne de cet algorithme de comparaison toohello Two-Class Boosted Decision Tree.</span><span class="sxs-lookup"><span data-stu-id="11ff6-157">We will compare how this algorithm performs in comparison toohello Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="11ff6-158">Copier et coller hello modules Train Model et le modèle de Score hello canevas.</span><span class="sxs-lookup"><span data-stu-id="11ff6-158">Copy and Paste hello modules Train Model and Score Model in hello canvas.</span></span>
4. <span data-ttu-id="11ff6-159">Hello de glisser **modèle Evaluate** module dans les algorithmes de hello deux toocompare hello canevas.</span><span class="sxs-lookup"><span data-stu-id="11ff6-159">Drag hello **Evaluate Model** module into hello canvas toocompare hello two algorithms.</span></span>
5. <span data-ttu-id="11ff6-160">**Exécutez** hello expérience.</span><span class="sxs-lookup"><span data-stu-id="11ff6-160">**Run** hello experiment.</span></span>
   <span data-ttu-id="11ff6-161">![Exécutez hello expérience][10]</span><span class="sxs-lookup"><span data-stu-id="11ff6-161">![Run hello experiment][10]</span></span>
6. <span data-ttu-id="11ff6-162">Cliquez sur le port de sortie hello bas hello du module de modèle Evaluate hello, puis cliquez sur visualiser.</span><span class="sxs-lookup"><span data-stu-id="11ff6-162">Click hello output port at hello bottom of hello Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="11ff6-163">![Visualiser les résultats de l’évaluation][11]</span><span class="sxs-lookup"><span data-stu-id="11ff6-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="11ff6-164">les métriques Hello fournies sont courbe ROC hello, n’oubliez pas de précision diagramme et courbe de courbes d’élévation.</span><span class="sxs-lookup"><span data-stu-id="11ff6-164">hello metrics provided are hello ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="11ff6-165">En examinant ces métriques, nous pouvons voir ce premier modèle hello effectué mieux que hello deuxième.</span><span class="sxs-lookup"><span data-stu-id="11ff6-165">Looking at these metrics, we can see that hello first model performed better than hello second one.</span></span> <span data-ttu-id="11ff6-166">toolook à hello que hello premier modèle a prédit, cliquez sur le port de sortie du modèle de Score de hello, puis cliquez sur visualiser.</span><span class="sxs-lookup"><span data-stu-id="11ff6-166">toolook at hello what hello first model predicted, click on output port of hello Score Model and click Visualize.</span></span>
<span data-ttu-id="11ff6-167">![Visualiser les résultats de la notation][12]</span><span class="sxs-lookup"><span data-stu-id="11ff6-167">![Visualize score results][12]</span></span>

<span data-ttu-id="11ff6-168">Vous verrez que deux colonnes supplémentaires ajoutées tooyour test dataset.</span><span class="sxs-lookup"><span data-stu-id="11ff6-168">You will see two more columns added tooyour test dataset.</span></span>

* <span data-ttu-id="11ff6-169">Les probabilités notées : probabilité que hello qu’un client est un acheteur potentiel.</span><span class="sxs-lookup"><span data-stu-id="11ff6-169">Scored Probabilities: hello likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="11ff6-170">Étiquettes évaluées : hello classification effectuée par modèle hello : acheteur de vélo (1) ou non (0).</span><span class="sxs-lookup"><span data-stu-id="11ff6-170">Scored Labels: hello classification done by hello model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="11ff6-171">Ce seuil de probabilité pour l’étiquetage a la valeur too50 % et peut être ajusté.</span><span class="sxs-lookup"><span data-stu-id="11ff6-171">This probability threshold for labeling is set too50% and can be adjusted.</span></span>

<span data-ttu-id="11ff6-172">Comparaison des colonnes de hello BikeBuyer (réel) avec hello Scored Labels (prédiction), vous pouvez voir le modèle de hello degré.</span><span class="sxs-lookup"><span data-stu-id="11ff6-172">Comparing hello column BikeBuyer (actual) with hello Scored Labels (prediction), you can see how well hello model has performed.</span></span> <span data-ttu-id="11ff6-173">Dans les étapes suivantes, vous pouvez utiliser cette prédictions toomake de modèle pour les nouveaux clients et publier ce modèle comme un service web ou écrire tooSQL de retour de résultats entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="11ff6-173">As next steps, you can use this model toomake predictions for new customers and publish this model as a web service or write results back tooSQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11ff6-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="11ff6-174">Next steps</span></span>
<span data-ttu-id="11ff6-175">toolearn plus sur la création de modèles, d’apprentissage prédictive font référence trop[tooMachine de présentation de formation sur Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="11ff6-175">toolearn more about building predictive machine learning models, refer too[Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>

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
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
