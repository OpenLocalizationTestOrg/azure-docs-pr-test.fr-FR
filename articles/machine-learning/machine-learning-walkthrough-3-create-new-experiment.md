---
title: "Étape 3 : Création d’une expérience Machine Learning | Microsoft Docs"
description: "Étape 3 du guide pas à pas du développement d'une solution prédictive : Création d'une expérience d'apprentissage dans Azure Machine Learning Studio."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: cd410316910bce76f5c915c06e83b24c034481b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="3814b-103">Étape 3 de la procédure pas à pas : création d’une expérience Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3814b-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="3814b-104">Voici la troisième étape de la procédure pas à pas [Développement d’une solution d’analyse prédictive avec Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="3814b-104">This is the third step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="3814b-105">Créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="3814b-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="3814b-106">Télécharger des données existantes</span><span class="sxs-lookup"><span data-stu-id="3814b-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="3814b-107">**Créer une expérience**</span><span class="sxs-lookup"><span data-stu-id="3814b-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="3814b-108">Former et évaluer les modèles</span><span class="sxs-lookup"><span data-stu-id="3814b-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="3814b-109">Déployer le service web</span><span class="sxs-lookup"><span data-stu-id="3814b-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="3814b-110">Accéder au service web</span><span class="sxs-lookup"><span data-stu-id="3814b-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="3814b-111">L’étape suivante de cette procédure pas à pas consiste à créer une expérience dans Machine Learning Studio, qui utilise le jeu de données que nous avons chargé.</span><span class="sxs-lookup"><span data-stu-id="3814b-111">The next step in this walkthrough is to create an experiment in Machine Learning Studio that uses the dataset we uploaded.</span></span>  

1. <span data-ttu-id="3814b-112">Dans Studio, cliquez sur **+NOUVEAU** en bas de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="3814b-112">In Studio, click **+NEW** at the bottom of the window.</span></span>
2. <span data-ttu-id="3814b-113">Sélectionnez **EXPÉRIENCE**, puis sélectionnez « Expérience vide ».</span><span class="sxs-lookup"><span data-stu-id="3814b-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Création d'une expérience][0]

2. <span data-ttu-id="3814b-115">Sélectionnez le nom d’expérience par défaut, situé en haut du canevas, et remplacez-le par un nom significatif.</span><span class="sxs-lookup"><span data-stu-id="3814b-115">Select the default experiment name at the top of the canvas and rename it to something meaningful.</span></span>

    ![Renommer l’expérience][5]
   
   > [!TIP]
   > <span data-ttu-id="3814b-117">Il est conseillé de compléter les champs **Résumé** et **Description** relatifs à l’expérience dans le volet **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="3814b-117">It's a good practice to fill in **Summary** and **Description** for the experiment in the **Properties** pane.</span></span> <span data-ttu-id="3814b-118">Ces propriétés vous donnent la possibilité de documenter l'expérience afin que toute personne la consultant ultérieurement comprenne vos objectifs et votre méthodologie.</span><span class="sxs-lookup"><span data-stu-id="3814b-118">These properties give you the chance to document the experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Propriétés de l’expérience][6]
   > 
3. <span data-ttu-id="3814b-120">Dans la palette des modules à gauche du canevas d'expérience, développez **Jeux de données enregistrés**.</span><span class="sxs-lookup"><span data-stu-id="3814b-120">In the module palette to the left of the experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="3814b-121">Recherchez le jeu de données que vous avez créé sous **My Datasets** (Mes jeux de données) et faites-le glisser sur la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="3814b-121">Find the dataset you created under **My Datasets** and drag it onto the canvas.</span></span> <span data-ttu-id="3814b-122">Vous pouvez également le rechercher en entrant son nom dans la zone **Rechercher** au-dessus de la palette.</span><span class="sxs-lookup"><span data-stu-id="3814b-122">You can also find the dataset by entering the name in the **Search** box above the palette.</span></span>  

    ![Ajouter le jeu de données à l’expérience][7]

## <a name="prepare-the-data"></a><span data-ttu-id="3814b-124">Préparation des données</span><span class="sxs-lookup"><span data-stu-id="3814b-124">Prepare the data</span></span>
<span data-ttu-id="3814b-125">Vous pouvez voir les 100 premières lignes de données et quelques informations statistiques concernant tout le jeu de données : pour ce faire, cliquez sur le port de sortie du jeu de données (le petit cercle en bas) et en sélectionnez **Visualiser**.</span><span class="sxs-lookup"><span data-stu-id="3814b-125">You can view the first 100 rows of the data and some statistical information for the whole dataset: Click the output port of the dataset (the small circle at the bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="3814b-126">Le fichier de données étant dépourvu d’en-têtes de colonne, Studio a fourni des en-têtes génériques (Col1, Col2, *etc.*).</span><span class="sxs-lookup"><span data-stu-id="3814b-126">Because the data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="3814b-127">Des en-têtes explicites ne sont pas essentiels pour créer un modèle, mais ils facilitent l’utilisation des données dans l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3814b-127">Good headings aren't essential to creating a model, but they make it easier to work with the data in the experiment.</span></span> <span data-ttu-id="3814b-128">En outre, lors de la publication de ce modèle dans un service web, les en-têtes permettent à l’utilisateur du service d’identifier les colonnes.</span><span class="sxs-lookup"><span data-stu-id="3814b-128">Also, when we eventually publish this model in a web service, the headings help identify the columns to the user of the service.</span></span>  

<span data-ttu-id="3814b-129">Nous pouvons ajouter des en-têtes de colonne en utilisant le module [Modifier les métadonnées][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="3814b-129">We can add column headings using the [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="3814b-130">Vous utilisez le module [Modifier les métadonnées][edit-metadata] pour modifier des métadonnées associées à un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="3814b-130">You use the [Edit Metadata][edit-metadata] module to change metadata associated with a dataset.</span></span> <span data-ttu-id="3814b-131">Dans ce cas, nous l’utilisons pour fournir des noms plus conviviaux pour les en-têtes de colonne.</span><span class="sxs-lookup"><span data-stu-id="3814b-131">In this case, we use it to provide more friendly names for column headings.</span></span> 

<span data-ttu-id="3814b-132">Pour utiliser [Modifier les métadonnées][edit-metadata], vous devez commencer par spécifier les colonnes à modifier (en l’occurrence, toutes). Ensuite, vous spécifiez l’action à effectuer sur ces colonnes (en l’occurrence, la modification de leurs en-têtes).</span><span class="sxs-lookup"><span data-stu-id="3814b-132">To use [Edit Metadata][edit-metadata], you first specify which columns to modify (in this case, all of them.) Next, you specify the action to be performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="3814b-133">Dans la palette des modules, tapez « métadonnées » dans la zone **Rechercher** .</span><span class="sxs-lookup"><span data-stu-id="3814b-133">In the module palette, type "metadata" in the **Search** box.</span></span> <span data-ttu-id="3814b-134">Le module [Modifier les métadonnées][edit-metadata] apparaît dans la liste des modules.</span><span class="sxs-lookup"><span data-stu-id="3814b-134">The [Edit Metadata][edit-metadata] appears in the module list.</span></span>

2. <span data-ttu-id="3814b-135">Cliquez sur le module [Modifier les métadonnées][edit-metadata] et faites-le glisser sur le canevas avant de le déposer sous le jeu de données que nous avons ajouté précédemment.</span><span class="sxs-lookup"><span data-stu-id="3814b-135">Click and drag the [Edit Metadata][edit-metadata] module onto the canvas and drop it below the dataset we added earlier.</span></span>

3. <span data-ttu-id="3814b-136">Connectez le jeu de données au module [Modifier les métadonnées][edit-metadata] : cliquez sur le port de sortie du jeu de données (le petit cercle en bas du jeu de données), faites glisser vers le port d’entrée de [Modifier les métadonnées][edit-metadata] (le petit cercle en haut du module), puis relâchez le bouton de la souris.</span><span class="sxs-lookup"><span data-stu-id="3814b-136">Connect the dataset to the [Edit Metadata][edit-metadata]: click the output port of the dataset (the small circle at the bottom of the dataset), drag to the input port of [Edit Metadata][edit-metadata] (the small circle at the top of the module), then release the mouse button.</span></span> <span data-ttu-id="3814b-137">Le jeu de données et le module restent connectés même si vous opérez des déplacements sur le canevas.</span><span class="sxs-lookup"><span data-stu-id="3814b-137">The dataset and module remain connected even if you move either around on the canvas.</span></span>
   
   <span data-ttu-id="3814b-138">L'expérience doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="3814b-138">The experiment should now look something like this:</span></span>  
   
   ![Ajout de Modifier les métadonnées][1]
   
   <span data-ttu-id="3814b-140">Le point d’exclamation rouge indique que nous n’avons pas encore défini les propriétés de ce module.</span><span class="sxs-lookup"><span data-stu-id="3814b-140">The red exclamation mark indicates that we haven't set the properties for this module yet.</span></span> <span data-ttu-id="3814b-141">Ce sera notre prochaine tâche.</span><span class="sxs-lookup"><span data-stu-id="3814b-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="3814b-142">Vous pouvez ajouter un commentaire dans un module en double-cliquant sur ce module, puis en saisissant du texte.</span><span class="sxs-lookup"><span data-stu-id="3814b-142">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="3814b-143">Ceci peut vous aider à voir d'un seul coup d'œil ce que fait chaque module dans votre expérience.</span><span class="sxs-lookup"><span data-stu-id="3814b-143">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="3814b-144">Dans ce cas, double-cliquez sur le module [Modifier les métadonnées][edit-metadata] et tapez le commentaire « Ajouter des en-têtes de colonne ».</span><span class="sxs-lookup"><span data-stu-id="3814b-144">In this case, double-click the [Edit Metadata][edit-metadata] module and type the comment "Add column headings".</span></span> <span data-ttu-id="3814b-145">Cliquez n’importe où sur le canevas pour fermer la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="3814b-145">Click anywhere else on the canvas to close the text box.</span></span> <span data-ttu-id="3814b-146">Pour afficher le commentaire, cliquez sur la flèche vers le bas sur le module.</span><span class="sxs-lookup"><span data-stu-id="3814b-146">To display the comment, click the down-arrow on the module.</span></span>
   > 
   > ![Module Modifier les métadonnées avec un commentaire ajouté][8]
   > 
4. <span data-ttu-id="3814b-148">Sélectionnez [Modifier les métadonnées][edit-metadata], puis, dans le panneau **Propriétés** à droite du canevas, cliquez sur **Lancer le sélecteur de colonne**.</span><span class="sxs-lookup"><span data-stu-id="3814b-148">Select [Edit Metadata][edit-metadata], and in the **Properties** pane to the right of the canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="3814b-149">Dans la boîte de dialogue **Sélectionner les colonnes**, sélectionnez toutes les lignes des **Colonnes disponibles** puis cliquez sur > pour les déplacer vers les **Colonnes sélectionnées**.</span><span class="sxs-lookup"><span data-stu-id="3814b-149">In the **Select columns** dialog, select all the rows in **Available Columns** and click > to move them to **Selected Columns**.</span></span>
   <span data-ttu-id="3814b-150">La boîte de dialogue doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="3814b-150">The dialog should look like this:</span></span>

   ![Sélecteur de colonnes avec toutes les colonnes sélectionnées][2]

6. <span data-ttu-id="3814b-152">Cliquez sur la coche **OK**.</span><span class="sxs-lookup"><span data-stu-id="3814b-152">Click the **OK** check mark.</span></span>

7. <span data-ttu-id="3814b-153">Dans le panneau **Propriétés**, recherchez le paramètre **Nouveaux noms de colonne**.</span><span class="sxs-lookup"><span data-stu-id="3814b-153">Back in the **Properties** pane, look for the **New column names** parameter.</span></span> <span data-ttu-id="3814b-154">Dans ce champ, entrez une liste de noms pour les 21 colonnes du jeu de données, séparés par des virgules et dans l’ordre de la colonne.</span><span class="sxs-lookup"><span data-stu-id="3814b-154">In this field, enter a list of names for the 21 columns in the dataset, separated by commas and in column order.</span></span> <span data-ttu-id="3814b-155">Vous pouvez obtenir le nom des colonnes dans la documentation du jeu de données sur le site web UCI ou, par commodité, vous pouvez copier et coller la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="3814b-155">You can obtain the columns names from the dataset documentation on the UCI website, or for convenience you can copy and paste the following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="3814b-156">Le volet Propriétés ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="3814b-156">The Properties pane looks like this:</span></span>
   
   ![Propriétés de Modifier les métadonnées][3]

> [!TIP]
> <span data-ttu-id="3814b-158">Si vous souhaitez vérifier les en-têtes de colonne, exécutez l’expérience (cliquez sur **EXÉCUTER** sous le canevas d’expérience).</span><span class="sxs-lookup"><span data-stu-id="3814b-158">If you want to verify the column headings, run the experiment (click **RUN** below the experiment canvas).</span></span> <span data-ttu-id="3814b-159">À la fin de l’exécution (une coche verte s’affiche sur [Modifier les métadonnées][edit-metadata]), cliquez sur le port de sortie du module [Modifier les métadonnées][edit-metadata] et sélectionnez **Visualiser**.</span><span class="sxs-lookup"><span data-stu-id="3814b-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click the output port of the [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="3814b-160">Vous pouvez voir la sortie de tous les modules en procédant de même pour afficher la progression des données dans l'expérience.</span><span class="sxs-lookup"><span data-stu-id="3814b-160">You can view the output of any module in the same way to view the progress of the data through the experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="3814b-161">Création de jeux de données d'apprentissage et de test</span><span class="sxs-lookup"><span data-stu-id="3814b-161">Create training and test datasets</span></span>
<span data-ttu-id="3814b-162">Nous avons besoin de certaines données pour former le modèle et d’autres pour le tester.</span><span class="sxs-lookup"><span data-stu-id="3814b-162">We need some data to train the model and some to test it.</span></span>
<span data-ttu-id="3814b-163">Ainsi, lors de l’étape suivante de l’expérience, nous divisons le jeu de données en deux jeux de données distincts : un pour la formation de notre modèle et l’autre pour le tester.</span><span class="sxs-lookup"><span data-stu-id="3814b-163">So in the next step of the experiment, we split the dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="3814b-164">Pour ce faire, nous utilisons le module [Fractionner les données][split].</span><span class="sxs-lookup"><span data-stu-id="3814b-164">To do this, we use the [Split Data][split] module.</span></span>  

1. <span data-ttu-id="3814b-165">Recherchez le module [Fractionner les données][split], faites-le glisser sur le canevas et connectez-le au module [Modifier les métadonnées][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="3814b-165">Find the [Split Data][split] module, drag it onto the canvas, and connect it to the [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="3814b-166">Par défaut, le rapport de division est 0,5 et le paramètre **Fractionnement aléatoire** est défini.</span><span class="sxs-lookup"><span data-stu-id="3814b-166">By default, the split ratio is 0.5 and the **Randomized split** parameter is set.</span></span> <span data-ttu-id="3814b-167">Cela signifie qu’une moitié aléatoire des données sort par un port du module [Fractionner les données][split] et l’autre moitié par l’autre port.</span><span class="sxs-lookup"><span data-stu-id="3814b-167">This means that a random half of the data is output through one port of the [Split Data][split] module, and half through the other.</span></span> <span data-ttu-id="3814b-168">Vous pouvez ajuster ces paramètres, de même que le paramètre **Valeur de départ aléatoire**, pour changer la répartition entre les données d’apprentissage et de test.</span><span class="sxs-lookup"><span data-stu-id="3814b-168">You can adjust these parameters, as well as the **Random seed** parameter, to change the split between training and testing data.</span></span> <span data-ttu-id="3814b-169">Pour cet exemple, nous ne changeons rien.</span><span class="sxs-lookup"><span data-stu-id="3814b-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="3814b-170">La propriété **Fraction de lignes dans le premier jeu de données de sortie** détermine la quantité de données qui est sortie par le port de sortie *gauche*.</span><span class="sxs-lookup"><span data-stu-id="3814b-170">The property **Fraction of rows in the first output dataset** determines how much of the data is output through the *left* output port.</span></span> <span data-ttu-id="3814b-171">Par exemple, si vous définissez le rapport sur 0,7, 70 % des données sont sorties par le port gauche et 30 % par le port droit.</span><span class="sxs-lookup"><span data-stu-id="3814b-171">For instance, if you set the ratio to 0.7, then 70% of the data is output through the left port and 30% through the right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="3814b-172">Double-cliquez sur le module [Fractionner les données][split] et entrez le commentaire « Fractionnement des données de formation/test de 50 % ».</span><span class="sxs-lookup"><span data-stu-id="3814b-172">Double-click the [Split Data][split] module and enter the comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="3814b-173">Nous pouvons utiliser les sorties du module [Fractionner les données][split] à notre gré, mais choisissons la sortie gauche pour les données d’apprentissage et la sortie droite pour les données de test.</span><span class="sxs-lookup"><span data-stu-id="3814b-173">We can use the outputs of the [Split Data][split] module however we like, but let's choose to use the left output as training data and the right output as testing data.</span></span>  

<span data-ttu-id="3814b-174">Comme indiqué lors de l’[étape précédente](machine-learning-walkthrough-2-upload-data.md), le coût d’une erreur consistant à classer un crédit à risque élevé comme étant à faible risque est cinq fois plus élevé que celui de l’erreur consistant à classer un crédit à faible risque comme étant à risque élevé.</span><span class="sxs-lookup"><span data-stu-id="3814b-174">As mentioned in the [previous step](machine-learning-walkthrough-2-upload-data.md), the cost of misclassifying a high credit risk as low is five times higher than the cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="3814b-175">Pour tenir compte de cela, nous générons un nouveau jeu de données qui reflète cette fonction de coût.</span><span class="sxs-lookup"><span data-stu-id="3814b-175">To account for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="3814b-176">Dans le nouveau jeu de données, chaque exemple à haut risque est répliqué cinq fois, alors que les exemples à faible risque ne sont pas répliqués.</span><span class="sxs-lookup"><span data-stu-id="3814b-176">In the new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="3814b-177">Nous pouvons procéder à la réplication en utilisant le code R :</span><span class="sxs-lookup"><span data-stu-id="3814b-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="3814b-178">Recherchez le module [Exécuter un script R][execute-r-script] et faites-le glisser sur le canevas de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="3814b-178">Find and drag the [Execute R Script][execute-r-script] module onto the experiment canvas.</span></span> 

2. <span data-ttu-id="3814b-179">Connectez le port de sortie gauche du module [Fractionner les données][split] au premier port d’entrée (« Dataset 1 ») du module [Exécuter un script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="3814b-179">Connect the left output port of the [Split Data][split] module to the first input port ("Dataset1") of the [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="3814b-180">Double-cliquez sur le module [Exécuter un script R][execute-r-script] et entrez le commentaire « Définir l’ajustement des coûts ».</span><span class="sxs-lookup"><span data-stu-id="3814b-180">Double-click the [Execute R Script][execute-r-script] module and enter the comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="3814b-181">Dans le volet **Propriétés**, supprimez le texte par défaut du paramètre **Script R**, puis entrez le script suivant :</span><span class="sxs-lookup"><span data-stu-id="3814b-181">In the **Properties** pane, delete the default text in the **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Script R dans le module Exécuter un script R][9]

<span data-ttu-id="3814b-183">Nous devons répéter cette opération de réplication pour chaque sortie du module [Fractionner les données][split] pour que les données d’apprentissage et de test aient le même ajustement des coûts.</span><span class="sxs-lookup"><span data-stu-id="3814b-183">We need to do this same replication operation for each output of the [Split Data][split] module so that the training and testing data have the same cost adjustment.</span></span> <span data-ttu-id="3814b-184">Pour ce faire, la manière la plus simple consiste à dupliquer le module [Exécuter un script R][execute-r-script] que nous venons de créer et à le connecter à l’autre port de sortie du module [Fractionner les données][split].</span><span class="sxs-lookup"><span data-stu-id="3814b-184">The easiest way to do this is by duplicating the [Execute R Script][execute-r-script] module we just made and connecting it to the other output port of the [Split Data][split] module.</span></span>

1. <span data-ttu-id="3814b-185">Cliquez avec le bouton droit sur le module [Exécuter un script R][execute-r-script] et sélectionnez **Copier**.</span><span class="sxs-lookup"><span data-stu-id="3814b-185">Right-click the [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="3814b-186">Cliquez avec le bouton droit sur le canevas d'expérience et sélectionnez **Coller**.</span><span class="sxs-lookup"><span data-stu-id="3814b-186">Right-click the experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="3814b-187">Faites glisser le nouveau module pour le mettre en place, puis connectez le port de sortie droit du module [Fractionner les données][split] au premier port d’entrée du module [Exécuter un script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="3814b-187">Drag the new module into position, and then connect the right output port of the [Split Data][split] module to the first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="3814b-188">En bas du canevas, cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="3814b-188">At the bottom of the canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="3814b-189">La copie du Module d’exécution de script R contient le même script que le module d’origine.</span><span class="sxs-lookup"><span data-stu-id="3814b-189">The copy of the Execute R Script module contains the same script as the original module.</span></span> <span data-ttu-id="3814b-190">Lorsque vous copiez-collez un module sur le canevas, la copie conserve toutes les propriétés de l'original.</span><span class="sxs-lookup"><span data-stu-id="3814b-190">When you copy and paste a module on the canvas, the copy retains all the properties of the original.</span></span>  
> 
> 

<span data-ttu-id="3814b-191">À ce stade, notre expérience ressemble à cela :</span><span class="sxs-lookup"><span data-stu-id="3814b-191">Our experiment now looks something like this:</span></span>

![Adding Split module and R scripts][4]

<span data-ttu-id="3814b-193">Pour plus d’informations sur l'utilisation de scripts R dans vos expériences, consultez la page [Prolonger votre expérience avec R](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="3814b-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="3814b-194">**Étape suivante : [Former et évaluer les modèles](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="3814b-194">**Next: [Train and evaluate the models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

[0]: ./media/machine-learning-walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/machine-learning-walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/machine-learning-walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/machine-learning-walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/machine-learning-walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/machine-learning-walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/machine-learning-walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
