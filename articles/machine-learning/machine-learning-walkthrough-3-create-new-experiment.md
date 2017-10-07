---
title: "Étape 3 : Création d’une expérience Machine Learning | Microsoft Docs"
description: "Étape 3 de hello développer la procédure pas à pas une solution prédictive : créer une nouvelle expérience de formation dans Azure Machine Learning Studio."
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
ms.openlocfilehash: 4697d461a205c50c8d2aa6a3bd56697840cb30f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="90dac-103">Étape 3 de la procédure pas à pas : création d’une expérience Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="90dac-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="90dac-104">Il s’agit hello troisième étape de hello procédure pas à pas, [développer une solution prédictive analytique dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="90dac-104">This is hello third step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="90dac-105">Créer un espace de travail Machine Learning</span><span class="sxs-lookup"><span data-stu-id="90dac-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="90dac-106">Télécharger des données existantes</span><span class="sxs-lookup"><span data-stu-id="90dac-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. <span data-ttu-id="90dac-107">**Créer une expérience**</span><span class="sxs-lookup"><span data-stu-id="90dac-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="90dac-108">L’apprentissage et évaluer des modèles de hello</span><span class="sxs-lookup"><span data-stu-id="90dac-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="90dac-109">Déployer le service Web de hello</span><span class="sxs-lookup"><span data-stu-id="90dac-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="90dac-110">Accéder au service Web de hello</span><span class="sxs-lookup"><span data-stu-id="90dac-110">Access hello Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="90dac-111">étape suivante de Hello dans cette procédure pas à pas est toocreate une expérience dans Machine Learning Studio qui utilise le jeu de données hello que nous téléchargés.</span><span class="sxs-lookup"><span data-stu-id="90dac-111">hello next step in this walkthrough is toocreate an experiment in Machine Learning Studio that uses hello dataset we uploaded.</span></span>  

1. <span data-ttu-id="90dac-112">Dans Studio, cliquez sur **+ nouveau** bas hello de fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-112">In Studio, click **+NEW** at hello bottom of hello window.</span></span>
2. <span data-ttu-id="90dac-113">Sélectionnez **EXPÉRIENCE**, puis sélectionnez « Expérience vide ».</span><span class="sxs-lookup"><span data-stu-id="90dac-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Création d'une expérience][0]

2. <span data-ttu-id="90dac-115">Par défaut de SELECT hello expérimenter nom haut hello de zone de dessin hello et renommez-la toosomething explicite.</span><span class="sxs-lookup"><span data-stu-id="90dac-115">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful.</span></span>

    ![Renommer l’expérience][5]
   
   > [!TIP]
   > <span data-ttu-id="90dac-117">Il est une bonne approche en matière toofill **Résumé** et **Description** pour expérience hello Bonjour **propriétés** volet.</span><span class="sxs-lookup"><span data-stu-id="90dac-117">It's a good practice toofill in **Summary** and **Description** for hello experiment in hello **Properties** pane.</span></span> <span data-ttu-id="90dac-118">Permettent de ces propriétés hello d’expérience de chance toodocument hello afin que toute personne qui consulte ultérieurement comprennent vos objectifs et la méthodologie.</span><span class="sxs-lookup"><span data-stu-id="90dac-118">These properties give you hello chance toodocument hello experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Propriétés de l’expérience][6]
   > 
3. <span data-ttu-id="90dac-120">Dans hello module palette toohello gauche du canevas de l’expérience hello, développez **jeux de données enregistrés**.</span><span class="sxs-lookup"><span data-stu-id="90dac-120">In hello module palette toohello left of hello experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="90dac-121">Rechercher hello dataset est créé sous **mes Datasets** et faites-le glisser sur le canevas de hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-121">Find hello dataset you created under **My Datasets** and drag it onto hello canvas.</span></span> <span data-ttu-id="90dac-122">Vous trouverez également hello dataset en entrant le nom de hello Bonjour **recherche** zone située au-dessus de la palette de hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-122">You can also find hello dataset by entering hello name in hello **Search** box above hello palette.</span></span>  

    ![Ajouter l’expérience de hello dataset toohello][7]

## <a name="prepare-hello-data"></a><span data-ttu-id="90dac-124">Préparer les données de salutation</span><span class="sxs-lookup"><span data-stu-id="90dac-124">Prepare hello data</span></span>
<span data-ttu-id="90dac-125">Vous pouvez afficher hello les 100 premières lignes de données de hello et quelques informations statistiques pour l’ensemble du dataset hello : cliquez sur le port de sortie hello du jeu de données hello (hello petit cercle bas hello) et sélectionnez **visualiser**.</span><span class="sxs-lookup"><span data-stu-id="90dac-125">You can view hello first 100 rows of hello data and some statistical information for hello whole dataset: Click hello output port of hello dataset (hello small circle at hello bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="90dac-126">Étant donné que le fichier de données hello n’était fourni avec des en-têtes de colonnes, Studio a fourni des en-têtes génériques (Col1, Col2, *etc.*).</span><span class="sxs-lookup"><span data-stu-id="90dac-126">Because hello data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="90dac-127">Bonne en-têtes ne sont pas essentiel toocreating un modèle, mais elles rendent toowork plus facile avec les données de salutation dans expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-127">Good headings aren't essential toocreating a model, but they make it easier toowork with hello data in hello experiment.</span></span> <span data-ttu-id="90dac-128">En outre, lorsque nous publions finalement ce modèle dans un service web, des en-têtes de hello aider à identifier hello colonnes toohello utilisateur du service de hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-128">Also, when we eventually publish this model in a web service, hello headings help identify hello columns toohello user of hello service.</span></span>  

<span data-ttu-id="90dac-129">Nous pouvons ajouter des en-têtes de colonnes à l’aide de hello [modifier les métadonnées] [ edit-metadata] module.</span><span class="sxs-lookup"><span data-stu-id="90dac-129">We can add column headings using hello [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="90dac-130">Vous utilisez hello [modifier les métadonnées] [ edit-metadata] métadonnées toochange module avec un jeu de données.</span><span class="sxs-lookup"><span data-stu-id="90dac-130">You use hello [Edit Metadata][edit-metadata] module toochange metadata associated with a dataset.</span></span> <span data-ttu-id="90dac-131">Dans ce cas, nous utilisons il tooprovide des noms plus conviviaux pour les en-têtes de colonne.</span><span class="sxs-lookup"><span data-stu-id="90dac-131">In this case, we use it tooprovide more friendly names for column headings.</span></span> 

<span data-ttu-id="90dac-132">toouse [modifier les métadonnées][edit-metadata], vous spécifiez tout d’abord le toomodify de colonnes (dans ce cas, tous les.) Ensuite, vous spécifiez hello action toobe est effectuée sur les colonnes (dans ce cas, la modification des en-têtes de colonne.)</span><span class="sxs-lookup"><span data-stu-id="90dac-132">toouse [Edit Metadata][edit-metadata], you first specify which columns toomodify (in this case, all of them.) Next, you specify hello action toobe performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="90dac-133">Dans la palette de module hello, tapez « métadonnées » Bonjour **recherche** boîte.</span><span class="sxs-lookup"><span data-stu-id="90dac-133">In hello module palette, type "metadata" in hello **Search** box.</span></span> <span data-ttu-id="90dac-134">Hello [modifier les métadonnées] [ edit-metadata] apparaît dans la liste des modules de hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-134">hello [Edit Metadata][edit-metadata] appears in hello module list.</span></span>

2. <span data-ttu-id="90dac-135">Cliquez et faites glisser hello [modifier les métadonnées] [ edit-metadata] module sur hello canevas et déposez-le sous le dataset hello ajouté précédemment.</span><span class="sxs-lookup"><span data-stu-id="90dac-135">Click and drag hello [Edit Metadata][edit-metadata] module onto hello canvas and drop it below hello dataset we added earlier.</span></span>

3. <span data-ttu-id="90dac-136">Se connecter hello dataset toohello [modifier les métadonnées][edit-metadata]: cliquez sur le port de sortie hello du jeu de données hello (hello petit cercle bas hello du jeu de données hello), faites glisser le port d’entrée toohello [modifier les métadonnées ] [ edit-metadata] (hello petit cercle haut hello du module de hello), puis relâchez le bouton de la souris hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-136">Connect hello dataset toohello [Edit Metadata][edit-metadata]: click hello output port of hello dataset (hello small circle at hello bottom of hello dataset), drag toohello input port of [Edit Metadata][edit-metadata] (hello small circle at hello top of hello module), then release hello mouse button.</span></span> <span data-ttu-id="90dac-137">module et le jeu de données hello restent connectés, même si vous soit déplacez sur la zone de dessin hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-137">hello dataset and module remain connected even if you move either around on hello canvas.</span></span>
   
   <span data-ttu-id="90dac-138">expérience de Hello doit maintenant ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="90dac-138">hello experiment should now look something like this:</span></span>  
   
   ![Ajout de Modifier les métadonnées][1]
   
   <span data-ttu-id="90dac-140">point d’exclamation Hello rouge indique que nous n’avons pas encore défini les propriétés hello pour ce module.</span><span class="sxs-lookup"><span data-stu-id="90dac-140">hello red exclamation mark indicates that we haven't set hello properties for this module yet.</span></span> <span data-ttu-id="90dac-141">Ce sera notre prochaine tâche.</span><span class="sxs-lookup"><span data-stu-id="90dac-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="90dac-142">Vous pouvez ajouter un module de tooa de commentaire par module de hello en double-cliquant sur et la saisie de texte.</span><span class="sxs-lookup"><span data-stu-id="90dac-142">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="90dac-143">Vous pouvez ainsi voir en un coup de œil quel module hello effectue dans votre expérience.</span><span class="sxs-lookup"><span data-stu-id="90dac-143">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="90dac-144">Dans ce cas, double-cliquez sur hello [modifier les métadonnées] [ edit-metadata] module et type hello commentaire « ajouter des en-têtes de colonnes ».</span><span class="sxs-lookup"><span data-stu-id="90dac-144">In this case, double-click hello [Edit Metadata][edit-metadata] module and type hello comment "Add column headings".</span></span> <span data-ttu-id="90dac-145">Cliquez sur n’importe où sur la zone de texte hello canevas tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-145">Click anywhere else on hello canvas tooclose hello text box.</span></span> <span data-ttu-id="90dac-146">toodisplay hello commentaire, cliquez sur la flèche hello sur le module de hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-146">toodisplay hello comment, click hello down-arrow on hello module.</span></span>
   > 
   > ![Module Modifier les métadonnées avec un commentaire ajouté][8]
   > 
4. <span data-ttu-id="90dac-148">Sélectionnez [modifier les métadonnées][edit-metadata]et Bonjour **propriétés** toohello volet à droite de la zone de dessin hello, cliquez sur **sélecteur de colonne lancement**.</span><span class="sxs-lookup"><span data-stu-id="90dac-148">Select [Edit Metadata][edit-metadata], and in hello **Properties** pane toohello right of hello canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="90dac-149">Bonjour **sélectionner des colonnes** boîte de dialogue, sélectionnez tous les hello lignes dans **colonnes disponibles** et cliquez sur > toomove les trop**colonnes sélectionnées**.</span><span class="sxs-lookup"><span data-stu-id="90dac-149">In hello **Select columns** dialog, select all hello rows in **Available Columns** and click > toomove them too**Selected Columns**.</span></span>
   <span data-ttu-id="90dac-150">boîte de dialogue Hello doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="90dac-150">hello dialog should look like this:</span></span>

   ![Sélecteur de colonnes avec toutes les colonnes sélectionnées][2]

6. <span data-ttu-id="90dac-152">Cliquez sur hello **OK** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="90dac-152">Click hello **OK** check mark.</span></span>

7. <span data-ttu-id="90dac-153">Dans hello **propriétés** volet, recherchez hello **nouveaux noms de colonnes** paramètre.</span><span class="sxs-lookup"><span data-stu-id="90dac-153">Back in hello **Properties** pane, look for hello **New column names** parameter.</span></span> <span data-ttu-id="90dac-154">Dans ce champ, entrez une liste de noms pour les colonnes de 21 hello dans dataset hello, séparés par des virgules et dans l’ordre des colonnes.</span><span class="sxs-lookup"><span data-stu-id="90dac-154">In this field, enter a list of names for hello 21 columns in hello dataset, separated by commas and in column order.</span></span> <span data-ttu-id="90dac-155">Vous pouvez obtenir les noms de colonnes hello à partir de la documentation du jeu de données hello sur le site Web de hello UCI, ou pour des raisons pratiques, vous pouvez copier et coller hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="90dac-155">You can obtain hello columns names from hello dataset documentation on hello UCI website, or for convenience you can copy and paste hello following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="90dac-156">volet de propriétés Hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="90dac-156">hello Properties pane looks like this:</span></span>
   
   ![Propriétés de Modifier les métadonnées][3]

> [!TIP]
> <span data-ttu-id="90dac-158">Si vous souhaitez que les en-têtes de colonne tooverify hello, exécutez l’expérience de hello (cliquez sur **exécuter** ci-dessous canevas de l’expérience hello).</span><span class="sxs-lookup"><span data-stu-id="90dac-158">If you want tooverify hello column headings, run hello experiment (click **RUN** below hello experiment canvas).</span></span> <span data-ttu-id="90dac-159">Lorsqu’il a terminé son exécution (une coche verte s’affiche sur [modifier les métadonnées][edit-metadata]), cliquez sur le port de sortie hello Hello [modifier les métadonnées] [ edit-metadata] module, puis sélectionnez **visualiser**.</span><span class="sxs-lookup"><span data-stu-id="90dac-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click hello output port of hello [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="90dac-160">Vous pouvez afficher la sortie de hello de n’importe quel module Bonjour même progression hello tooview de façon des données hello via une expérience de hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-160">You can view hello output of any module in hello same way tooview hello progress of hello data through hello experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="90dac-161">Création de jeux de données d'apprentissage et de test</span><span class="sxs-lookup"><span data-stu-id="90dac-161">Create training and test datasets</span></span>
<span data-ttu-id="90dac-162">Nous avons besoin de certains modèles hello tootrain et certains tootest il.</span><span class="sxs-lookup"><span data-stu-id="90dac-162">We need some data tootrain hello model and some tootest it.</span></span>
<span data-ttu-id="90dac-163">Afin de l’étape suivante de hello d’expérimentation de hello, nous fractionné hello le jeu de données en deux jeux de données distincts : un pour l’apprentissage de notre modèle et l’autre pour le tester.</span><span class="sxs-lookup"><span data-stu-id="90dac-163">So in hello next step of hello experiment, we split hello dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="90dac-164">toodo, nous utilisons hello [données fractionnées] [ split] module.</span><span class="sxs-lookup"><span data-stu-id="90dac-164">toodo this, we use hello [Split Data][split] module.</span></span>  

1. <span data-ttu-id="90dac-165">Recherche hello [données fractionnées] [ split] module, faites glisser sur la zone de dessin hello et connectez-la toohello [modifier les métadonnées] [ edit-metadata] module.</span><span class="sxs-lookup"><span data-stu-id="90dac-165">Find hello [Split Data][split] module, drag it onto hello canvas, and connect it toohello [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="90dac-166">Par défaut, les taux de fractionnement hello est 0,5 et hello **aléatoire fractionnement** paramètre est défini.</span><span class="sxs-lookup"><span data-stu-id="90dac-166">By default, hello split ratio is 0.5 and hello **Randomized split** parameter is set.</span></span> <span data-ttu-id="90dac-167">Cela signifie qu’une moitié aléatoire de données de salutation est sortie via un port de hello [données fractionnées] [ split] module et demi hello et autres.</span><span class="sxs-lookup"><span data-stu-id="90dac-167">This means that a random half of hello data is output through one port of hello [Split Data][split] module, and half through hello other.</span></span> <span data-ttu-id="90dac-168">Vous pouvez ajuster ces paramètres, mais aussi hello **valeur initiale aléatoire** paramètre hello toochange fractionnée entre les jeux d’apprentissage et de données de test.</span><span class="sxs-lookup"><span data-stu-id="90dac-168">You can adjust these parameters, as well as hello **Random seed** parameter, toochange hello split between training and testing data.</span></span> <span data-ttu-id="90dac-169">Pour cet exemple, nous ne changeons rien.</span><span class="sxs-lookup"><span data-stu-id="90dac-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="90dac-170">Hello propriété **Fraction de lignes Bonjour tout d’abord de sortie dataset** détermine la quantité de données de hello sortie via hello est *gauche* port de sortie.</span><span class="sxs-lookup"><span data-stu-id="90dac-170">hello property **Fraction of rows in hello first output dataset** determines how much of hello data is output through hello *left* output port.</span></span> <span data-ttu-id="90dac-171">Par exemple, si vous définissez hello ratio too0.7, 70 % des données de salutation est sortie via hello gauche de port et 30 % via le port de droite hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-171">For instance, if you set hello ratio too0.7, then 70% of hello data is output through hello left port and 30% through hello right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="90dac-172">Double-cliquez sur hello [données fractionnées] [ split] module et entrez le commentaire hello, « fractionnement les données de test de formation/50 % ».</span><span class="sxs-lookup"><span data-stu-id="90dac-172">Double-click hello [Split Data][split] module and enter hello comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="90dac-173">Nous pouvons utiliser des sorties hello Hello [données fractionnées] [ split] comme test de données de sortie de module toutefois nous à, mais nous allons choisir toouse hello sortie gauche en tant que données d’apprentissage et hello à droite.</span><span class="sxs-lookup"><span data-stu-id="90dac-173">We can use hello outputs of hello [Split Data][split] module however we like, but let's choose toouse hello left output as training data and hello right output as testing data.</span></span>  

<span data-ttu-id="90dac-174">Comme mentionné dans hello [étape précédente](machine-learning-walkthrough-2-upload-data.md), coût hello de classer par erreur entrées un risque élevé comme faible est cinq fois supérieur à celui de hello classer par erreur entrées un risque de crédit basse aussi élevée.</span><span class="sxs-lookup"><span data-stu-id="90dac-174">As mentioned in hello [previous step](machine-learning-walkthrough-2-upload-data.md), hello cost of misclassifying a high credit risk as low is five times higher than hello cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="90dac-175">tooaccount pour cela, nous générons un nouveau jeu de données qui reflète cette fonction de coût.</span><span class="sxs-lookup"><span data-stu-id="90dac-175">tooaccount for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="90dac-176">Hello le nouveau jeu de données, chaque exemple de risque élevé est répliquée cinq fois, tandis que chaque exemple de risque faible n’est pas répliquée.</span><span class="sxs-lookup"><span data-stu-id="90dac-176">In hello new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="90dac-177">Nous pouvons procéder à la réplication en utilisant le code R :</span><span class="sxs-lookup"><span data-stu-id="90dac-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="90dac-178">Rechercher et faites glisser hello [Execute R Script] [ execute-r-script] module sur le canevas de l’expérience hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-178">Find and drag hello [Execute R Script][execute-r-script] module onto hello experiment canvas.</span></span> 

2. <span data-ttu-id="90dac-179">Se connecter hello gauche du port de sortie de hello [données fractionnées] [ split] module toohello premier port d’entrée (« Dataset1 ») de hello [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="90dac-179">Connect hello left output port of hello [Split Data][split] module toohello first input port ("Dataset1") of hello [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="90dac-180">Double-cliquez sur hello [Execute R Script] [ execute-r-script] module et entrez le commentaire hello, « Ajustement des coûts de la plage ».</span><span class="sxs-lookup"><span data-stu-id="90dac-180">Double-click hello [Execute R Script][execute-r-script] module and enter hello comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="90dac-181">Bonjour **propriétés** volet, supprimer le texte par défaut hello Bonjour **Script R** paramètre et entrez ce script :</span><span class="sxs-lookup"><span data-stu-id="90dac-181">In hello **Properties** pane, delete hello default text in hello **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![Script R dans le module Execute R Script de hello][9]

<span data-ttu-id="90dac-183">Nous avons besoin de cette même opération de réplication pour chaque sortie hello toodo [données fractionnées] [ split] module afin que hello d’apprentissage et de données de test ont hello même ajustement des coûts.</span><span class="sxs-lookup"><span data-stu-id="90dac-183">We need toodo this same replication operation for each output of hello [Split Data][split] module so that hello training and testing data have hello same cost adjustment.</span></span> <span data-ttu-id="90dac-184">Hello plus simple façon toodo, il s’agit en dupliquant hello [Execute R Script] [ execute-r-script] module nous vient et sa connexion toohello autre sortie de port de hello [données fractionnées] [ split] module.</span><span class="sxs-lookup"><span data-stu-id="90dac-184">hello easiest way toodo this is by duplicating hello [Execute R Script][execute-r-script] module we just made and connecting it toohello other output port of hello [Split Data][split] module.</span></span>

1. <span data-ttu-id="90dac-185">Avec le bouton hello [Execute R Script] [ execute-r-script] module et sélectionnez **copie**.</span><span class="sxs-lookup"><span data-stu-id="90dac-185">Right-click hello [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="90dac-186">Cliquez sur le canevas de l’expérience hello et sélectionnez **coller**.</span><span class="sxs-lookup"><span data-stu-id="90dac-186">Right-click hello experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="90dac-187">Faites glisser nouveau module de hello en position et puis connectez le port de sortie de droite hello Hello [données fractionnées] [ split] module toohello premier port d’entrée de ce nouveau [Execute R Script] [ execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="90dac-187">Drag hello new module into position, and then connect hello right output port of hello [Split Data][split] module toohello first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="90dac-188">Au bas de hello du canevas de hello, cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="90dac-188">At hello bottom of hello canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="90dac-189">copie Hello du module Execute R Script de hello contienne hello même script en tant que module d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="90dac-189">hello copy of hello Execute R Script module contains hello same script as hello original module.</span></span> <span data-ttu-id="90dac-190">Lorsque vous copiez et collez un module dans la zone de dessin hello, copie de hello conserve toutes les propriétés de hello Hello d’origine.</span><span class="sxs-lookup"><span data-stu-id="90dac-190">When you copy and paste a module on hello canvas, hello copy retains all hello properties of hello original.</span></span>  
> 
> 

<span data-ttu-id="90dac-191">À ce stade, notre expérience ressemble à cela :</span><span class="sxs-lookup"><span data-stu-id="90dac-191">Our experiment now looks something like this:</span></span>

![Adding Split module and R scripts][4]

<span data-ttu-id="90dac-193">Pour plus d’informations sur l'utilisation de scripts R dans vos expériences, consultez la page [Prolonger votre expérience avec R](machine-learning-extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="90dac-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](machine-learning-extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="90dac-194">**Ensuite : [Train et évaluer des modèles de hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="90dac-194">**Next: [Train and evaluate hello models](machine-learning-walkthrough-4-train-and-evaluate-models.md)**</span></span>

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
