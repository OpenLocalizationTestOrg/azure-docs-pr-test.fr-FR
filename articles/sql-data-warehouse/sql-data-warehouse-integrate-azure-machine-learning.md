---
title: "aaaUse Azure Machine Learning avec l’entrepôt de données SQL | Documents Microsoft"
description: "Didacticiel sur l’utilisation de Microsoft Azure Machine Learning avec Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="0f5df-103">Utilisation de Microsoft Azure Machine Learning avec SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0f5df-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="0f5df-104">Azure Machine Learning est un service entièrement géré analytique prédictives que vous pouvez utiliser les modèles prédictifs toocreate par rapport à vos données dans l’entrepôt de données SQL et puis publier en tant que services web de prêt à consommer.</span><span class="sxs-lookup"><span data-stu-id="0f5df-104">Azure Machine Learning is a fully managed predictive analytics service that you can use toocreate predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="0f5df-105">Vous pouvez les principes fondamentaux d’analytique prédictive hello et apprentissage en lisant [tooMachine de présentation de formation sur Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="0f5df-105">You can learn hello basics of predictive analytics and machine learning by reading [Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>  <span data-ttu-id="0f5df-106">Vous pouvez ensuite apprendre comment toocreate, l’apprentissage, évaluer et tester un modèle d’apprentissage automatique à l’aide de hello [créer expérience didacticiel][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="0f5df-106">You can then learn how toocreate, train, score and test a machine learning model using hello [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="0f5df-107">Dans cet article, vous allez apprendre comment hello toodo suivant à l’aide de hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="0f5df-107">In this article, you will learn how toodo hello following using hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="0f5df-108">Les données lues à partir de votre base de données toocreate, effectuer l’apprentissage et le score d’un modèle de prévision</span><span class="sxs-lookup"><span data-stu-id="0f5df-108">Read data from your database toocreate, train and score a predictive model</span></span>
* <span data-ttu-id="0f5df-109">Écriture de base de données tooyour de données</span><span class="sxs-lookup"><span data-stu-id="0f5df-109">Write data tooyour database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="0f5df-110">Lire des données à partir de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0f5df-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="0f5df-111">Données seront lues à partir de la table Product dans la base de données AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-111">We will read data from Product table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="0f5df-112">Étape 1</span><span class="sxs-lookup"><span data-stu-id="0f5df-112">Step 1</span></span>
<span data-ttu-id="0f5df-113">Démarrez une nouvelle expérience en cliquant sur + Nouveau bas hello hello fenêtre de la Machine Learning Studio, sélectionnez expérience, puis faire des essais vide.</span><span class="sxs-lookup"><span data-stu-id="0f5df-113">Start a new experiment by clicking +NEW at hello bottom of hello Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="0f5df-114">Par défaut de hello sélectionnez expérimenter nom haut hello de zone de dessin hello et renommez-la toosomething explicite, par exemple, les prédiction de prix de bicyclette.</span><span class="sxs-lookup"><span data-stu-id="0f5df-114">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="0f5df-115">Étape 2</span><span class="sxs-lookup"><span data-stu-id="0f5df-115">Step 2</span></span>
<span data-ttu-id="0f5df-116">Recherchez le module de lecture hello dans la palette hello des jeux de données et les modules sur gauche hello du canevas de l’expérience hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-116">Look for hello Reader module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="0f5df-117">Faites glisser le canevas de l’expérience toohello module hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-117">Drag hello module toohello experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="0f5df-118">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="0f5df-118">Step 3</span></span>
<span data-ttu-id="0f5df-119">Sélectionnez le module de lecture hello et remplir le volet de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-119">Select hello Reader module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="0f5df-120">Sélectionnez la base de données SQL Azure en tant que Source de données de hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-120">Select Azure SQL Database as hello Data Source.</span></span>
2. <span data-ttu-id="0f5df-121">Nom du serveur de base de données : nom de serveur de Type hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-121">Database server name: Type hello server name.</span></span> <span data-ttu-id="0f5df-122">Vous pouvez utiliser hello [portail Azure] [ Azure portal] toofind cela.</span><span class="sxs-lookup"><span data-stu-id="0f5df-122">You can use hello [Azure portal][Azure portal] toofind this.</span></span>

![][server_name]

1. <span data-ttu-id="0f5df-123">Nom de la base de données : nom hello du Type de base de données sur le serveur hello vous venez de spécifier.</span><span class="sxs-lookup"><span data-stu-id="0f5df-123">Database name: Type hello name of a database on hello server you just specified.</span></span>
2. <span data-ttu-id="0f5df-124">Nom du compte utilisateur Server : nom d’utilisateur de Type hello d’un compte qui dispose des autorisations d’accès pour la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-124">Server user account name:  Type hello user name of an account that has access permissions for hello database.</span></span>
3. <span data-ttu-id="0f5df-125">Mot de passe utilisateur Server : fournir un mot de passe hello pour hello de compte d’utilisateur spécifié.</span><span class="sxs-lookup"><span data-stu-id="0f5df-125">Server user account password: Provide hello password for hello specified user account.</span></span>
4. <span data-ttu-id="0f5df-126">Accepter n’importe quel certificat du serveur : utilisez cette option (moins sûr) si vous souhaitez tooskip examiner le certificat de site hello avant de lire vos données.</span><span class="sxs-lookup"><span data-stu-id="0f5df-126">Accept any server certificate: Use this option (less secure) if you want tooskip reviewing hello site certificate before you read your data.</span></span>
5. <span data-ttu-id="0f5df-127">Requête de base de données : entrez une instruction SQL qui décrit les données hello tooread.</span><span class="sxs-lookup"><span data-stu-id="0f5df-127">Database query: Enter a SQL statement that describes hello data you want tooread.</span></span> <span data-ttu-id="0f5df-128">Dans ce cas, nous lira des données à partir de la table Product à l’aide de hello suivant la requête.</span><span class="sxs-lookup"><span data-stu-id="0f5df-128">In this case, we will read data from Product table using hello following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="0f5df-129">Étape 4</span><span class="sxs-lookup"><span data-stu-id="0f5df-129">Step 4</span></span>
1. <span data-ttu-id="0f5df-130">Exécutez hello expérience en cliquant sur Exécuter dans le canevas de l’expérience hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-130">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="0f5df-131">Fin de l’expérience de hello, module de lecture hello aura un tooindicate de coche verte a terminé avec succès.</span><span class="sxs-lookup"><span data-stu-id="0f5df-131">When hello experiment finishes, hello Reader module will have a green check mark tooindicate that it has completed successfully.</span></span> <span data-ttu-id="0f5df-132">Notez également hello vous avez terminé de l’état en cours d’exécution dans le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-132">Notice also hello Finished running status in hello upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="0f5df-133">toosee hello des données importées, cliquez sur le port de sortie hello bas hello du jeu de données automobile hello et sélectionnez visualiser.</span><span class="sxs-lookup"><span data-stu-id="0f5df-133">toosee hello imported data, click hello output port at hello bottom of hello automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="0f5df-134">Créer, former et évaluer un modèle</span><span class="sxs-lookup"><span data-stu-id="0f5df-134">Create, train and score a model</span></span>
<span data-ttu-id="0f5df-135">Vous pouvez désormais utiliser ce jeu de données pour effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="0f5df-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="0f5df-136">Créer un modèle : traiter des données et définir des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="0f5df-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="0f5df-137">Modèle de hello train : choisissez d’appliquer un algorithme d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="0f5df-137">Train hello model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="0f5df-138">Score et test de modèle hello : prédire nouveau prix de bicyclette</span><span class="sxs-lookup"><span data-stu-id="0f5df-138">Score and test hello model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="0f5df-139">toolearn plus en détail comment toocreate, l’apprentissage, évaluer et tester un hello d’utilisation de modèle d’apprentissage [créer expérience didacticiel][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="0f5df-139">toolearn more about how toocreate, train, score and test a machine learning model use hello [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-tooazure-sql-data-warehouse"></a><span data-ttu-id="0f5df-140">Écrire des données tooAzure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0f5df-140">Write data tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="0f5df-141">Nous écrirons hello résultat ensemble tooProductPriceForecast table dans la base de données AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-141">We will write hello result set tooProductPriceForecast table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="0f5df-142">Étape 1</span><span class="sxs-lookup"><span data-stu-id="0f5df-142">Step 1</span></span>
<span data-ttu-id="0f5df-143">Recherchez le module de Writer hello dans la palette hello des jeux de données et les modules sur gauche hello du canevas de l’expérience hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-143">Look for hello Writer module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="0f5df-144">Faites glisser le canevas de l’expérience toohello module hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-144">Drag hello module toohello experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="0f5df-145">Étape 2</span><span class="sxs-lookup"><span data-stu-id="0f5df-145">Step 2</span></span>
<span data-ttu-id="0f5df-146">Sélectionnez le module de Writer hello et remplir le volet de propriétés hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-146">Select hello Writer module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="0f5df-147">Sélectionnez base de données SQL Azure comme Destination des données de hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-147">Select Azure SQL Database as hello Data Destination.</span></span>
2. <span data-ttu-id="0f5df-148">Nom du serveur de base de données : nom de serveur de Type hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-148">Database server name: Type hello server name.</span></span> <span data-ttu-id="0f5df-149">Vous pouvez utiliser hello [portail Azure] [ Azure portal] toofind cela.</span><span class="sxs-lookup"><span data-stu-id="0f5df-149">You can use hello [Azure portal][Azure portal] toofind this.</span></span>
3. <span data-ttu-id="0f5df-150">Nom de la base de données : nom hello du Type de base de données sur le serveur hello vous venez de spécifier.</span><span class="sxs-lookup"><span data-stu-id="0f5df-150">Database name: Type hello name of a database on hello server you just specified.</span></span>
4. <span data-ttu-id="0f5df-151">Nom du compte utilisateur Server : nom d’utilisateur de Type hello d’un compte qui dispose des autorisations d’écriture pour la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-151">Server user account name:  Type hello user name of an account that has write permissions for hello database.</span></span>
5. <span data-ttu-id="0f5df-152">Mot de passe utilisateur Server : fournir un mot de passe hello pour hello de compte d’utilisateur spécifié.</span><span class="sxs-lookup"><span data-stu-id="0f5df-152">Server user account password: Provide hello password for hello specified user account.</span></span>
6. <span data-ttu-id="0f5df-153">Accepter n’importe quel certificat du serveur (non sécurisé) : sélectionnez cette option si vous ne souhaitez pas certificat de hello tooview.</span><span class="sxs-lookup"><span data-stu-id="0f5df-153">Accept any server certificate (insecure): Select this option if you don’t want tooview hello certificate.</span></span>
7. <span data-ttu-id="0f5df-154">Séparées par des virgules de liste de toobe colonnes enregistré : fournir une liste de colonnes de jeu de données ou le résultat de hello que vous souhaitez toooutput.</span><span class="sxs-lookup"><span data-stu-id="0f5df-154">Comma-separated list of columns toobe saved: Provide a list of hello dataset or result columns that you want toooutput.</span></span>
8. <span data-ttu-id="0f5df-155">Nom de table de données : spécifiez le nom hello de table de données hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-155">Data table name: Specify hello name of hello data table.</span></span>
9. <span data-ttu-id="0f5df-156">Séparées par des virgules de liste de colonnes de la table de données : spécifiez toouse de noms de colonne hello dans la nouvelle table de hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-156">Comma-separated list of datatable columns:  Specify hello column names toouse in hello new table.</span></span> <span data-ttu-id="0f5df-157">Hello les noms de colonne peuvent être différents de hello ceux qui sont dans le jeu de données source hello, mais vous devez répertorier hello même nombre de colonnes ici que vous définissez pour la table de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-157">hello column names can be different from hello ones in hello source dataset, but you must list hello same number of columns here that you define for hello output table.</span></span>
10. <span data-ttu-id="0f5df-158">Nombre de lignes écrites par opération SQL Azure : vous pouvez configurer le nombre de hello de lignes écrites tooa base de données SQL en une seule opération.</span><span class="sxs-lookup"><span data-stu-id="0f5df-158">Number of rows written per SQL Azure operation: You can configure hello number of rows that are written tooa SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="0f5df-159">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="0f5df-159">Step 3</span></span>
1. <span data-ttu-id="0f5df-160">Exécutez hello expérience en cliquant sur Exécuter dans le canevas de l’expérience hello.</span><span class="sxs-lookup"><span data-stu-id="0f5df-160">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="0f5df-161">Fin de l’expérience de hello, tous les modules aura un tooindicate de coche verte avec succès.</span><span class="sxs-lookup"><span data-stu-id="0f5df-161">When hello experiment finishes, all modules will have a green check mark tooindicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f5df-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0f5df-162">Next steps</span></span>
<span data-ttu-id="0f5df-163">Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="0f5df-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
