---
title: Utilisation de Microsoft Azure Machine Learning avec SQL Data Warehouse | Documents Microsoft
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
ms.openlocfilehash: c19860c6b5b1c15d1e29ddc67f9cf9ad4618725b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="3b154-103">Utilisation de Microsoft Azure Machine Learning avec SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3b154-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="3b154-104">Azure Machine Learning est un service d’analyse prédictive entièrement géré qui vous permet de développer des modèles d’analyse prédictive de vos données dans SQL Data Warehouse et de les publier en tant que services Web prêts à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="3b154-104">Azure Machine Learning is a fully managed predictive analytics service that you can use to create predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="3b154-105">Pour découvrir les principes de base de l’analyse prédictive et de Machine Learning, consultez l’[Introduction à Machine Learning sur Microsoft Azure][Introduction to Machine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="3b154-105">You can learn the basics of predictive analytics and machine learning by reading [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>  <span data-ttu-id="3b154-106">Vous pouvez ensuite apprendre à créer, former, évaluer et tester un modèle Machine Learning à l’aide du [didacticiel consacré à la création d’une expérience][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="3b154-106">You can then learn how to create, train, score and test a machine learning model using the [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="3b154-107">Dans cet article, vous allez apprendre à effectuer les opérations suivantes en utilisant [Azure Machine Learning Studio][Azure Machine Learning Studio] :</span><span class="sxs-lookup"><span data-stu-id="3b154-107">In this article, you will learn how to do the following using the [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="3b154-108">Lire des données à partir de votre base de données pour créer, former et évaluer un modèle d’analyse prédictive</span><span class="sxs-lookup"><span data-stu-id="3b154-108">Read data from your database to create, train and score a predictive model</span></span>
* <span data-ttu-id="3b154-109">Écrire des données dans votre base de données</span><span class="sxs-lookup"><span data-stu-id="3b154-109">Write data to your database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="3b154-110">Lire des données à partir de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3b154-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="3b154-111">Nous lirons les données de la table Product dans la base de données AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="3b154-111">We will read data from Product table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="3b154-112">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="3b154-112">Step 1</span></span>
<span data-ttu-id="3b154-113">Démarrez une nouvelle expérience en cliquant sur l’option + NOUVEAU située en bas de la fenêtre de Machine Learning Studio, sélectionnez EXPÉRIENCE, puis « Expérience vide ».</span><span class="sxs-lookup"><span data-stu-id="3b154-113">Start a new experiment by clicking +NEW at the bottom of the Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="3b154-114">Sélectionnez le nom d’expérience par défaut, situé en haut de la zone de dessin, et remplacez-le par un nom significatif, par exemple : Prédiction de prix d’un vélo.</span><span class="sxs-lookup"><span data-stu-id="3b154-114">Select the default experiment name at the top of the canvas and rename it to something meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="3b154-115">Étape 2 :</span><span class="sxs-lookup"><span data-stu-id="3b154-115">Step 2</span></span>
<span data-ttu-id="3b154-116">Recherchez le module Lecteur dans la palette d’ensemble de données et de modules située sur la gauche de la zone de dessin d’expérience.</span><span class="sxs-lookup"><span data-stu-id="3b154-116">Look for the Reader module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="3b154-117">Faites glisser le module sur la zone de dessin d’expérience.</span><span class="sxs-lookup"><span data-stu-id="3b154-117">Drag the module to the experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="3b154-118">Étape 3</span><span class="sxs-lookup"><span data-stu-id="3b154-118">Step 3</span></span>
<span data-ttu-id="3b154-119">Sélectionnez le module Lecteur et renseignez le panneau des propriétés.</span><span class="sxs-lookup"><span data-stu-id="3b154-119">Select the Reader module and fill out the properties pane.</span></span>

1. <span data-ttu-id="3b154-120">Sélectionnez la base de données SQL Azure en tant que source de données.</span><span class="sxs-lookup"><span data-stu-id="3b154-120">Select Azure SQL Database as the Data Source.</span></span>
2. <span data-ttu-id="3b154-121">Nom du serveur de base de données : tapez le nom du serveur.</span><span class="sxs-lookup"><span data-stu-id="3b154-121">Database server name: Type the server name.</span></span> <span data-ttu-id="3b154-122">Vous pouvez obtenir cette information dans le [portail Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="3b154-122">You can use the [Azure portal][Azure portal] to find this.</span></span>

![][server_name]

1. <span data-ttu-id="3b154-123">Nom de la base de données : tapez le nom d’une base de données sur le serveur que vous venez de définir.</span><span class="sxs-lookup"><span data-stu-id="3b154-123">Database name: Type the name of a database on the server you just specified.</span></span>
2. <span data-ttu-id="3b154-124">Nom du compte utilisateur du serveur : tapez le nom d’utilisateur d’un compte disposant des autorisations d’accès à la base de données.</span><span class="sxs-lookup"><span data-stu-id="3b154-124">Server user account name:  Type the user name of an account that has access permissions for the database.</span></span>
3. <span data-ttu-id="3b154-125">Mot de passe du compte utilisateur du serveur : renseignez le mot de passe du compte utilisateur spécifié.</span><span class="sxs-lookup"><span data-stu-id="3b154-125">Server user account password: Provide the password for the specified user account.</span></span>
4. <span data-ttu-id="3b154-126">Accepter un certificat de serveur : utilisez cette option (moins sûre) si vous ne souhaitez pas consulter le certificat du site avant de lire les données.</span><span class="sxs-lookup"><span data-stu-id="3b154-126">Accept any server certificate: Use this option (less secure) if you want to skip reviewing the site certificate before you read your data.</span></span>
5. <span data-ttu-id="3b154-127">Requête de base de données : tapez une instruction SQL qui décrit les données que vous souhaitez lire.</span><span class="sxs-lookup"><span data-stu-id="3b154-127">Database query: Enter a SQL statement that describes the data you want to read.</span></span> <span data-ttu-id="3b154-128">Dans ce cas, nous lirons les données de la table Product à l’aide de la requête suivante.</span><span class="sxs-lookup"><span data-stu-id="3b154-128">In this case, we will read data from Product table using the following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="3b154-129">Étape 4</span><span class="sxs-lookup"><span data-stu-id="3b154-129">Step 4</span></span>
1. <span data-ttu-id="3b154-130">Démarrez l’expérience en cliquant sur l’option Démarrer sous la zone de dessin de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3b154-130">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="3b154-131">Une fois l’expérience terminée, une coche verte s’affiche en regard du module Lecteur pour indiquer la réussite des opérations.</span><span class="sxs-lookup"><span data-stu-id="3b154-131">When the experiment finishes, the Reader module will have a green check mark to indicate that it has completed successfully.</span></span> <span data-ttu-id="3b154-132">Notez que le statut Exécution terminée s’affiche dans le coin supérieur droit de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="3b154-132">Notice also the Finished running status in the upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="3b154-133">Pour voir à quoi ressemblent les données importées, cliquez sur le port de sortie situé en bas du jeu de données d’automobile, puis sélectionnez Visualiser.</span><span class="sxs-lookup"><span data-stu-id="3b154-133">To see the imported data, click the output port at the bottom of the automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="3b154-134">Créer, former et évaluer un modèle</span><span class="sxs-lookup"><span data-stu-id="3b154-134">Create, train and score a model</span></span>
<span data-ttu-id="3b154-135">Vous pouvez désormais utiliser ce jeu de données pour effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="3b154-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="3b154-136">Créer un modèle : traiter des données et définir des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3b154-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="3b154-137">Former le modèle : sélectionner et appliquer un algorithme d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="3b154-137">Train the model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="3b154-138">Évaluer et tester le modèle : prédire le nouveau prix d’un vélo.</span><span class="sxs-lookup"><span data-stu-id="3b154-138">Score and test the model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="3b154-139">Pour en savoir plus sur la création, la formation, l’évaluation et le test d’un modèle Machine Learning, utilisez le [didacticiel consacré à la création d’une expérience][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="3b154-139">To learn more about how to create, train, score and test a machine learning model use the [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-to-azure-sql-data-warehouse"></a><span data-ttu-id="3b154-140">Écrire des données sur Microsoft Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3b154-140">Write data to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="3b154-141">Nous écrirons l’ensemble de résultats sur la table ProductPriceForecast de la base de données AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="3b154-141">We will write the result set to ProductPriceForecast table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="3b154-142">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="3b154-142">Step 1</span></span>
<span data-ttu-id="3b154-143">Recherchez le module Lecteur dans la palette d’ensemble de données et de modules située sur la gauche de la zone de dessin d’expérience.</span><span class="sxs-lookup"><span data-stu-id="3b154-143">Look for the Writer module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="3b154-144">Faites glisser le module sur la zone de dessin d’expérience.</span><span class="sxs-lookup"><span data-stu-id="3b154-144">Drag the module to the experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="3b154-145">Étape 2 :</span><span class="sxs-lookup"><span data-stu-id="3b154-145">Step 2</span></span>
<span data-ttu-id="3b154-146">Sélectionnez le module Lecteur et renseignez le volet des propriétés.</span><span class="sxs-lookup"><span data-stu-id="3b154-146">Select the Writer module and fill out the properties pane.</span></span>

1. <span data-ttu-id="3b154-147">Sélectionnez la base de données SQL Microsoft Azure en tant que Destination des données.</span><span class="sxs-lookup"><span data-stu-id="3b154-147">Select Azure SQL Database as the Data Destination.</span></span>
2. <span data-ttu-id="3b154-148">Nom du serveur de base de données : tapez le nom du serveur.</span><span class="sxs-lookup"><span data-stu-id="3b154-148">Database server name: Type the server name.</span></span> <span data-ttu-id="3b154-149">Vous pouvez obtenir cette information dans le [portail Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="3b154-149">You can use the [Azure portal][Azure portal] to find this.</span></span>
3. <span data-ttu-id="3b154-150">Nom de la base de données : tapez le nom d’une base de données sur le serveur que vous venez de définir.</span><span class="sxs-lookup"><span data-stu-id="3b154-150">Database name: Type the name of a database on the server you just specified.</span></span>
4. <span data-ttu-id="3b154-151">Nom du compte utilisateur du serveur : tapez le nom d’utilisateur d’un compte disposant des autorisations d’écriture sur la base de données.</span><span class="sxs-lookup"><span data-stu-id="3b154-151">Server user account name:  Type the user name of an account that has write permissions for the database.</span></span>
5. <span data-ttu-id="3b154-152">Mot de passe du compte utilisateur du serveur : renseignez le mot de passe du compte utilisateur spécifié.</span><span class="sxs-lookup"><span data-stu-id="3b154-152">Server user account password: Provide the password for the specified user account.</span></span>
6. <span data-ttu-id="3b154-153">Accepter un certificat de serveur (non sûre) : sélectionnez cette option si vous ne souhaitez pas consulter le certificat.</span><span class="sxs-lookup"><span data-stu-id="3b154-153">Accept any server certificate (insecure): Select this option if you don’t want to view the certificate.</span></span>
7. <span data-ttu-id="3b154-154">Liste de colonnes séparées par des virgules à enregistrer : fournit une liste de l’ensemble de données ou des colonnes de résultats que vous souhaitez générer.</span><span class="sxs-lookup"><span data-stu-id="3b154-154">Comma-separated list of columns to be saved: Provide a list of the dataset or result columns that you want to output.</span></span>
8. <span data-ttu-id="3b154-155">Nom de table de données : spécifiez ici le nom de la table de données.</span><span class="sxs-lookup"><span data-stu-id="3b154-155">Data table name: Specify the name of the data table.</span></span>
9. <span data-ttu-id="3b154-156">Liste des colonnes de la table de données, séparées par des virgules : spécifiez les noms de colonne à utiliser dans la nouvelle table.</span><span class="sxs-lookup"><span data-stu-id="3b154-156">Comma-separated list of datatable columns:  Specify the column names to use in the new table.</span></span> <span data-ttu-id="3b154-157">Les noms des colonnes peuvent être différents de ceux de l’ensemble de données source, mais vous devez indiquer les noms de colonnes définis pour la table de sortie.</span><span class="sxs-lookup"><span data-stu-id="3b154-157">The column names can be different from the ones in the source dataset, but you must list the same number of columns here that you define for the output table.</span></span>
10. <span data-ttu-id="3b154-158">Nombre de lignes écrites par opération SQL Azure : vous pouvez configurer le nombre de lignes écrites sur une base de données SQL lors d’une opération.</span><span class="sxs-lookup"><span data-stu-id="3b154-158">Number of rows written per SQL Azure operation: You can configure the number of rows that are written to a SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="3b154-159">Étape 3</span><span class="sxs-lookup"><span data-stu-id="3b154-159">Step 3</span></span>
1. <span data-ttu-id="3b154-160">Démarrez l’expérience en cliquant sur l’option Démarrer sous la zone de dessin de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3b154-160">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="3b154-161">Une fois l’expérience terminée, une coche verte s’affiche en regard de chaque module pour indiquer la réussite de leurs opérations.</span><span class="sxs-lookup"><span data-stu-id="3b154-161">When the experiment finishes, all modules will have a green check mark to indicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b154-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b154-162">Next steps</span></span>
<span data-ttu-id="3b154-163">Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="3b154-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Introduction to machine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
